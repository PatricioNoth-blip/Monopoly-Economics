# 03 – Technische Architektur (Vorschlag)

> Status: **Vorschlag, noch nicht freigegeben.** Code entsteht erst nach der Freigabe.

## 1. Kurzfassung

- **TypeScript überall**: Server, Browser und Spiellogik sprechen dieselbe Sprache.
- **Spiellogik als reiner Rechenkern** (`engine`): keine Datenbank, kein Netzwerk,
  nur Regeln. Dadurch vollständig testbar, und Balancing-Simulationen werden möglich.
- **Ein autoritativer Server** (Node.js) verarbeitet jede Aktion, prüft sie mit
  der Engine, speichert sie und verteilt den neuen Stand **per WebSocket** sofort
  an alle Geräte.
- **PostgreSQL** speichert ein unveränderliches **Ereignisprotokoll** jeder Partie.
  Daraus ergeben sich Spielstand, Transaktionshistorie und „Warum?“-Erklärungen.
- **React-WebApp (PWA)**, Mobile First, mit eigenen Layouts für Smartphone, iPad und
  Desktop. Ohne Installation nutzbar, optional zum Home-Bildschirm hinzufügbar.

---

## 2. Was die Architektur treibt

| Anforderung | Konsequenz |
|---|---|
| Alle Geräte sehen sofort denselben Stand | Server schickt Änderungen aktiv (WebSocket), keine Abfragen im Sekundentakt |
| Der Server vertraut dem Browser nicht | Der Browser sendet nur **Absichten** („kaufe 5 Aktien“); Preise, Mieten und Werte rechnet ausschließlich der Server |
| Nichts darf verloren gehen | Jede Aktion wird gespeichert, **bevor** sie verteilt wird |
| Lückenlose Historie | Unveränderliches Ereignisprotokoll; Korrekturen sind Gegenbuchungen |
| „Warum hat sich X geändert?“ | Bewertung und Miete liefern immer eine Aufschlüsselung, nicht nur eine Zahl |
| Gleichzeitige Aktionen (letzte Aktie) | Aktionen einer Partie laufen strikt nacheinander |
| Doppeltipp / Funkloch | Jede Aktion hat eine eindeutige ID und wird höchstens einmal ausgeführt |
| Regeln ändern sich durchs Balancing | Regelwerk ist versioniert und parametrisiert; jede Partie speichert ihre Regeln |

---

## 3. Optionen im Vergleich

| Option | Echtzeit | Wo liegt die Spiellogik? | Betrieb | Abhängigkeit | Fazit |
|---|---|---|---|---|---|
| **Eigener Node-Server + PostgreSQL + WebSocket** | ✔ | TypeScript, gleiche Engine wie im Browser | 1 Container + DB | keine | **Empfehlung** |
| Supabase (Postgres + Realtime) | ✔ | SQL-Funktionen oder Edge Functions | sehr gering | mittel | Stark bei einfachen Datenänderungen. Komplexe Regeln (Bewertung, Kreisprüfung, Insolvenz) in SQL sind aber schwer zu testen, und die Logik verteilt sich |
| Firebase / Firestore | ✔ | Cloud Functions | gering | hoch | Verleitet zu direkten Client-Schreibzugriffen, schwache Transaktionen über mehrere Dokumente |
| Convex | ✔ (reaktiv) | TypeScript-Funktionen, transaktional | sehr gering | mittel–hoch | **Ernsthafte Alternative**, falls du gar keinen Server betreiben willst |
| Cloudflare Durable Objects / PartyKit | ✔ | TypeScript pro Spielraum | gering | hoch | Passt sehr elegant zu „ein Raum pro Partie“, aber Nischen-Ökosystem |

**Warum der eigene Server?** Bei diesem Spiel steckt die Komplexität in den
**Regeln**, nicht in der Datenmenge. Ich will die Regeln an genau einer Stelle
haben (der Engine), mit tausenden Tests und Simulationen absichern und überall
wiederverwenden. Ein schlanker eigener Server macht das am einfachsten,
funktioniert lokal ohne Cloud-Konto und bindet uns an keinen Anbieter. Die Last ist
winzig (eine Handvoll Partien mit je ≤ 10 Geräten), dafür reicht eine einzige
kleine Server-Instanz.

> **Was ist ein WebSocket?** Eine dauerhaft offene Leitung zwischen Gerät und
> Server. Der Server kann darüber jederzeit von sich aus Neuigkeiten schicken.
> Deshalb muss niemand neu laden.

---

## 4. Gesamtbild

```
 📱 iPhone      📱 iPad (Bank)      💻 Desktop      📺 Tischansicht (später)
     │               │                  │                 │
     └──────── WebSocket (Socket.IO) + HTTPS ─────────────┘
                              │
              ┌───────────────▼────────────────┐
              │        Server (Node.js)        │
              │  ┌──────────────────────────┐  │
              │  │ Auth & Sitzungen          │  │  Login Bank, Beitritt Spieler
              │  ├──────────────────────────┤  │
              │  │ Spielraum je Partie       │  │  Warteschlange: 1 Aktion nach der anderen
              │  │   └─ Engine (Regeln)      │  │  prüfen → Ereignisse erzeugen
              │  ├──────────────────────────┤  │
              │  │ Verteiler                 │  │  neuen Stand an alle Geräte der Partie
              │  └──────────────────────────┘  │
              └───────────────┬────────────────┘
                              │
                    ┌─────────▼─────────┐
                    │    PostgreSQL     │  Ereignisprotokoll, Snapshots,
                    │                   │  Spieler/Sitzungen, Bank-Accounts
                    └───────────────────┘
```

---

## 5. Der Rechenkern (`packages/engine`)

Die gesamte Spiellogik besteht aus **reinen Funktionen**:

```ts
// Prüft eine Aktion gegen Regeln + Rechte und liefert Ereignisse oder einen Regelverstoß.
decide(state, command, actor): Ereignis[] | Regelverstoß

// Wendet ein Ereignis auf den Zustand an (deterministisch).
apply(state, event): State

// Abgeleitete Werte, immer mit Aufschlüsselung:
valuation(state, companyId) → { total, substanz[], ertrag[], kurs }
rent(state, propertyId, ctx) → { total, positionen[] }
```

- **Keine Zufallszahlen in der Engine.** Würfelt die App, erzeugt der Server die
  Zahl und legt sie im Ereignis ab. Jede Partie lässt sich so exakt nachspielen.
- **Rechte sind Teil der Regeln:** `decide` prüft auch, ob *dieser* Akteur das
  darf. Es gibt also genau eine Stelle für Berechtigungen.
- **Regelparameter** (Gründungsgebühr, Multiplikator, Projektkatalog …) kommen aus
  einem versionierten Regelwerk. Die Bank wählt beim Erstellen ein Preset.

### Invarianten (werden nach **jeder** Aktion automatisch geprüft und getestet)
1. Die Aktienzahl jeder Firma bleibt konstant (Summe aller Besitzer + Reserve + Bankbestand = 100).
2. Kein Konto eines Spielers oder einer Firma ist jemals negativ.
3. Jede Geldbewegung hat Quelle und Ziel (doppelte Buchführung). Geld entsteht und
   verschwindet nur über das Bank-Konto.
4. Jede Straße hat genau einen Besitzer (Bank, Spieler oder Firma).
5. Projekt-Slots sind nie überbelegt.
6. Der Beteiligungsgraph ist kreisfrei.
7. Das Protokoll wird nur ergänzt, nie verändert.

---

## 6. Weg einer Aktion: „Patty kauft 10 Aktien TECH“

```
Patty (iPhone)                Server: Spielraum ABC123                 PostgreSQL     alle Geräte
     │  befehl {id: 7f3…, typ: AktienKaufen,                                │              │
     │          firma: TECH, stück: 10, erwarteterKurs: 112}                │              │
     ├──────────────────────────────►│                                    │              │
     │                               │ 1. Sitzung prüfen (wer ist das?)    │              │
     │                               │ 2. Format prüfen (Schema)           │              │
     │                               │ 3. In die Warteschlange der Partie  │              │
     │                               │ 4. engine.decide → Ereignisse       │              │
     │                               │    (Kurs noch 112? Geld da? Aktien  │              │
     │                               │     im Angebot? Patty darf das?)    │              │
     │                               │ 5. Ereignisse speichern ───────────►│ Transaktion  │
     │                               │ 6. Zustand aktualisieren            │              │
     │                               │ 7. neuen Stand verteilen ──────────────────────────►│
     │◄──────────── Bestätigung ─────┤                                    │              │
```

- **`erwarteterKurs`**: Hat sich der Kurs zwischen Anzeige und Tippen geändert,
  lehnt der Server ab („Kurs ist inzwischen 115 M, trotzdem kaufen?“). Niemand
  zahlt also unbemerkt einen anderen Preis.
- **Befehls-ID**: Kommt dieselbe Aktion zweimal an (Doppeltipp, Funkloch), wird sie
  nur einmal ausgeführt und die erste Antwort wiederholt.
- **Speichern vor Verteilen**: Schlägt das Speichern fehl, ändert sich nichts, und
  der Spieler bekommt eine Fehlermeldung.

---

## 7. Echtzeit-Synchronisation

**Grundsatz: lieber robust als clever.** Ein Spielstand ist klein (geschätzt
< 100 KB). Nach jeder Änderung schickt der Server deshalb den **vollständigen
Stand** mit einer fortlaufenden Versionsnummer, dazu die neuen Protokolleinträge
für Benachrichtigungen. Fehleranfällige Teil-Updates, bei denen ein Gerät aus dem
Tritt geraten kann, gibt es nicht. Optimieren können wir später, falls nötig.

- **Wiederverbinden:** Das Gerät meldet seine letzte Version. Ist sie veraltet,
  bekommt es sofort den aktuellen Stand.
- **iPhone/iPad im Hintergrund:** iOS kappt Verbindungen von Hintergrund-Tabs. Beim
  Zurückkehren (`visibilitychange`) verbindet die App sofort neu und gleicht ab.
- **Verbindungsanzeige:** Ein kleiner Status zeigt „verbunden“ oder „verbinde …“.
  Ohne Verbindung sind Geld-Aktionen gesperrt. Es gibt bewusst **keine**
  Offline-Warteschlange, damit keine Zahlung Minuten später überraschend ausgeführt
  wird.
- **Keine optimistischen Anzeigen bei Geld:** Die App zeigt kurz „wird
  ausgeführt …“ und dann das echte Ergebnis vom Server (typisch < 200 ms).
- **Sichtbarkeit:** Der Server erzeugt die Sicht pro Gerät über eine Funktion
  `sichtFür(state, betrachter)`. Bei „alles öffentlich“ (G-06) ist sie für alle
  gleich, private Kontostände wären aber jederzeit nachrüstbar.

---

## 8. Speicherung

**Ereignisprotokoll + Snapshots** („Event Sourcing light“):

| Tabelle | Inhalt |
|---|---|
| `bank_users` | Bank-Accounts (Benutzername, Passwort-Hash) |
| `games` | Partie: Code, Status, Bank, Regelwerk-Version + Parameter |
| `players` | Spieler einer Partie: Nickname, Status, Sitzungsschlüssel (gehasht), optional `user_id` für spätere Accounts |
| `game_events` | **Das Herzstück:** fortlaufend nummerierte Ereignisse je Partie (`game_id`, `seq`, `command_id`, Akteur, Typ, Daten, Zeit). Eindeutig je (`game_id`, `seq`) und (`game_id`, `command_id`) |
| `game_snapshots` | Kompletter Zustand alle ~100 Ereignisse, damit der Server nach einem Neustart schnell lädt |

Warum so?
- Die **Transaktionshistorie** ist einfach das lesbar aufbereitete Protokoll.
- **„Warum?“-Erklärungen** entstehen aus Vorher/Nachher-Vergleichen.
- **Nichts wird überschrieben**. Fehler werden durch Gegenbuchungen korrigiert.
- **Server-Neustart?** Snapshot laden, restliche Ereignisse anwenden, weiter.
- **Fehlersuche:** Jede echte Partie lässt sich lokal Schritt für Schritt nachspielen.

---

## 9. Fachliches Datenmodell

```
Partie ─┬─ Spieler ──────────── Konto
        ├─ Firma ──┬─────────── Konto (Firmenkasse)
        │          ├─ Aktienbesitz (Inhaber: Spieler | Firma | Reserve | Bankbestand)
        │          └─ Projekte ─── auf Straße, belegt Slots
        ├─ Straße (statisch: Brettdaten) + Zustand (Besitzer, Gebäude, Hypothek)
        ├─ Buchung (von Konto → an Konto, Betrag, Art, Bezug, Akteur)
        ├─ Handelsangebot (Paket: Geld/Aktien/Straßen, Status)
        ├─ Marktplatz-Angebot (Firma, Stück, Preis, Verkäufer)
        ├─ Mietforderung (Straße, Zahler, Betrag + Aufschlüsselung, Status)
        ├─ Antrag/Abstimmung (Firma, Gegenstand, Stimmen)
        ├─ Quartal (Nummer, Konjunktur, Bericht)
        └─ Ereigniskarte (Firma, Art, Wirkung, Quartal)
```

**Zahlenregeln**
- Geld ist immer eine **ganze Zahl in M**. Keine Kommazahlen, keine
  Rundungsfehler.
- Anteile werden aus Stückzahlen berechnet, nie als Kommazahl gespeichert.
- Dividenden werden pro Aktie **abgerundet**; der Rest bleibt in der Firmenkasse.
- Die Bank ist ein Konto ohne Untergrenze (Geldquelle und Geldsenke).

---

## 10. Sicherheit & Rechte

| Aktion | Bank | Spieler (selbst) | CEO (für Firma) | Aktionär |
|---|:-:|:-:|:-:|:-:|
| Partie starten/pausieren/beenden, Quartal abschließen | ✔ | – | – | – |
| Ein-/Auszahlung, Korrekturbuchung | ✔ | – | – | – |
| Grundbuch-Eintrag („gekauft“) | ✔ | ✔ | – | – |
| Mietforderung stellen / bezahlen | ✔ | ✔ / ✔ | ✔ / – | – |
| Firma gründen | – | ✔ | – | – |
| Bauen, Projekte, Dividende, Reserve anbieten | – | – | ✔ | – |
| Aktien kaufen/verkaufen, Handelsangebot | – | ✔ | ✔ | ✔ |
| Abstimmen | – | – | ✔ | ✔ |
| Spieler sperren/entfernen, Wiederbeitritts-Code | ✔ | – | – | – |

- **Sitzungen:** zufälliger 256-Bit-Schlüssel pro Gerät, in der DB nur gehasht
  gespeichert, nur über HTTPS.
- **Bank-Passwort:** sicher gehasht (Argon2).
- **Eingaben:** Jede Nachricht wird gegen ein Schema geprüft (Zod). Beträge sind
  ganzzahlig, positiv und begrenzt. Unbekannte Felder werden abgelehnt.
- **Der Browser rechnet nie verbindlich.** Er darf Vorschauen anzeigen, die Zahl im
  Protokoll stammt aber immer vom Server.
- **Rate-Limits** für Beitrittsversuche (Codes erraten) und Aktionen pro Gerät.

---

## 11. Frontend & UI-Grundkonzept (Entwurf)

**Technik:** React + Vite + TypeScript, Tailwind CSS, barrierearme
UI-Bausteine (Radix), PWA-fähig. Die Engine läuft auch im Browser, z. B. für
Vorschauen („Nach dem Kauf: 7.330 M“).

**Smartphone** – eine Hand, Daumen unten:
```
┌─────────────────────────┐
│ PATTY        ● verbunden│
│ 8.450 M                 │
├─────────────────────────┤
│ Vermögen 14.720 M  +3 % │
│ ┌ TECH   30 %   112 ▲ ┐ │
│ └ RETAIL 15 %    87 ▼ ┘ │
│ 🔔 Max fordert 1.200 M  │
│    Miete  [Bezahlen]    │
├─────────────────────────┤
│ 🏠   📈   [＋]   🏢   🧾 │
└─────────────────────────┘
```

**iPad (quer)** – Seitenleiste + Liste/Detail statt gestreckter Handyseite:
```
┌────────┬──────────────────┬─────────────────────────────┐
│ PATTY  │ Firmen           │ 🏢 TECH AG                  │
│ 8.450 M│ ▸ TECH    112 ▲  │ Wert 11.200 M   Kurs 112 M  │
│        │   RETAIL   87 ▼  │ ── Warum? ───────────────── │
│ Übers. │   BAU AG   54 ─  │ +800 Hotel · +500 Mieten …  │
│ Markt  │                  │ Aktionäre  Patty 60 % …     │
│ Firmen │                  │ Straßen & Slots [▣▣□] …     │
│ Verlauf│                  │ [Aktien kaufen] [Handeln]   │
└────────┴──────────────────┴─────────────────────────────┘
```

**Bank (typisch auf dem iPad):** links der Eingang (zu bestätigende Ein- und
Auszahlungen, Streitfälle, Beitrittsanfragen), rechts Spielerliste mit
Schnellbuchung über einen Ziffernblock (+100, +500 …) und Spielsteuerung
(Quartal, Pause).

**Bedienprinzipien**
- Tippflächen ≥ 44 px, nichts hängt am Mauszeiger.
- Aktionen öffnen eine Bottom-Sheet-Maske mit Zusammenfassung vor dem Bestätigen:
  „Du kaufst 10 TECH für 1.120 M. Danach: 7.330 M.“
- **Jede Zahl ist antippbar → „Warum?“** mit Aufschlüsselung.
- Geänderte Werte blinken kurz grün oder rot; eingehende Ereignisse erscheinen als
  Hinweis.
- Deutsche Zahlenformate („8.450 M“), Hell- und Dunkelmodus.
- **Später:** eine **Tischansicht** für TV oder iPad in der Tischmitte
  (Börsenticker, Quartalsbericht, Konjunktur).

Das ausführliche UI-Konzept folgt als eigener Schritt (`05-ui-konzept.md`).

---

## 12. Tests

| Ebene | Werkzeug | Was |
|---|---|---|
| Engine – Regeln | Vitest | Jede Regel, jeder Sonderfall. Die **Rechenbeispiele aus den Docs werden Tests** |
| Engine – Invarianten | fast-check (Property-Tests) | Tausende zufällige Aktionsfolgen; danach müssen alle Invarianten (§5) gelten |
| Balancing | eigene Simulation | Bot-Partien zur Kalibrierung: Spieldauer, Gewinnrate je Strategie, Geldmenge, Amortisation der Projekte |
| Server | Vitest + echte PostgreSQL | Gleichzeitige Aktionen, doppelte Befehle, Neustart, Wiederverbinden |
| Ende-zu-Ende | Playwright | Mehrere Geräte gleichzeitig (iPhone-, iPad-, Desktop-Profile): Aktion auf A ist in < 1 s auf B sichtbar |
| Realität | Testpartie | Checkliste und Notizen nach jeder echten Runde |

---

## 13. Betrieb

- **Ein Docker-Container** (Server liefert auch die WebApp aus) + **PostgreSQL**.
- Hosting z. B. Fly.io, Railway, Render oder ein kleiner VPS (Hetzner). Wichtig ist
  eine **immer laufende** Instanz, denn Gratis-Angebote, die einschlafen,
  verzögern den ersten Aufruf.
- Kosten realistisch: 0–10 € pro Monat.
- Tägliches DB-Backup; dank Ereignisprotokoll ist jede Partie rekonstruierbar.
- Lokal entwickeln: `docker compose up` startet die Datenbank, ohne Cloud-Konto.

---

## 14. Geplante Projektstruktur

```
apps/
  server/          Node.js: HTTP + WebSocket, Sitzungen, Spielräume, Speicherung
  web/             React-PWA für Spieler und Bank
packages/
  engine/          Regeln, Bewertung, Mieten – reine Logik, keine I/O
  protocol/        Befehle, Ereignisse, Nachrichten (gemeinsame Schemas)
tools/
  sim/             Balancing-Simulation auf Basis der Engine
data/
  board/           Brettdaten der Mega-Edition (board.json)
docs/              Konzept, Entscheidungen, Architektur
```
Paketverwaltung: pnpm-Workspaces (ein Repository, mehrere Pakete).

---

## 15. Vorgehen in Etappen

| Etappe | Inhalt | Ergebnis |
|---|---|---|
| **0** | Konzept, Analyse, Architektur | ✅ dieses Dokument |
| **1** | Entscheidungen klären, Regelwerk v0.1, `board.json` | Freigegebene Regeln |
| **2** | Engine + Tests + erste Simulation (noch ohne Oberfläche) | Regeln rechnen nachweislich korrekt |
| **3** | **Technischer Durchstich:** Lobby, Beitritt, Bank, Konten, Ein-/Auszahlung, Überweisung, Verlauf, Echtzeit | Mehrere Handys sehen live dasselbe |
| **4** | Wirtschaft: Grundbuch, Gründung, Aktien, Bewertung, Firmenmiete, Bauen, Dividenden, Quartal | Spielbare Kernversion |
| **5** | Projekte, Ereignisse, Konjunktur, Notverkauf/Insolvenz | **Erste vollständige Testpartie** |
| **6+** | Beteiligungen, Tischansicht, Statistiken, Accounts, Volldigital-Modus | Ausbau nach Testerfahrung |

Etappe 3 kommt bewusst früh: Die Echtzeit-Synchronisation über mehrere Geräte ist
das größte technische Risiko und soll sich bewähren, bevor viel Spiellogik daran
hängt.

---

## 16. Technische Risiken

| Risiko | Gegenmaßnahme |
|---|---|
| iOS beendet Hintergrund-Verbindungen | Neuverbindung und Abgleich beim Zurückkehren, Verbindungsanzeige |
| Ein Server = ein Ausfallpunkt | Zustand ist sofort gespeichert; nach Neustart verbinden sich die Geräte automatisch neu |
| Brett und App laufen auseinander | Grundbuch, Bank-Korrekturen, Erklärungen zu jeder Zahl |
| Regeländerungen brechen laufende Partien | Regelwerk-Version und Parameter werden pro Partie gespeichert |
| Zu viel Tipparbeit am Tisch | Jede Aktion ≤ 3 Taps als Designziel; Testpartien messen das |
