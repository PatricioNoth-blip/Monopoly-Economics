# 05 – UI-Konzept (Entwurf)

> Schritt 6 des Plans. Beschreibt Struktur, Abläufe und Bedienprinzipien, noch
> nicht das endgültige Aussehen. Die Wireframes zeigen Aufbau und Inhalt, nicht
> Farben oder Schriften. Offene UI-Fragen stehen am Ende (IDs `UI-…`).

---

## 1. Leitlinien

1. **Das Brett bleibt die Bühne.** Ein Blick aufs Handy dauert Sekunden. Deshalb
   gibt es große Zahlen und immer einen klaren nächsten Schritt.
2. **Häufiges in höchstens 3 Taps.** Seltenes darf ein geführter Assistent sein.
3. **Jede Zahl erklärt sich.** Antippen öffnet „Warum?“ mit der Aufschlüsselung.
4. **Kein Geld bewegt sich unbemerkt.** Eigene Zahlungen bestätigt man selbst,
   eingehende Buchungen werden angezeigt.
5. **Alle sehen dieselbe Wahrheit.** Ist ein Gerät offline, sagt es das, statt
   veraltete Zahlen als aktuell zu zeigen.

## 2. Wer nutzt was

| Rolle | Typisches Gerät | Haltung | Nutzung |
|---|---|---|---|
| Spieler | Smartphone | hochkant, eine Hand | kurze Blicke: Miete, Aktien, Kontostand |
| Bank (Spielleiter) | iPad | quer, liegt offen auf dem Tisch | dauerhaft: Ein-/Auszahlungen, Freigaben, Quartal |
| Tischansicht (später) | TV oder iPad in der Mitte | nur Anzeige | Börsenticker, Quartalsbericht |

## 3. Was am Tisch wie oft passiert

Die Häufigkeit bestimmt, wie prominent eine Aktion ist.

| Aktion | Wer | Häufigkeit | Ziel | Einstieg |
|---|---|---|---|---|
| Firmenmiete bezahlen | Spieler | sehr oft | 1 Tap | Forderung erscheint von selbst |
| Firmenmiete melden/fordern | Zahler, CEO, jeder | sehr oft | 2–3 Taps | ＋ → „Miete“ |
| Straße ins Grundbuch eintragen | Spieler | oft (früh im Spiel) | 2–3 Taps | ＋ → „Straße gekauft“ |
| Ein-/Auszahlung | Bank | oft | 3 Taps | Spieler antippen → Betrag |
| Aktien kaufen/verkaufen | Spieler | mittel | 3 Taps | Börse → Firma |
| Bauen für die Firma | CEO | mittel | 3 Taps | Firma → Verwalten |
| Quartal abschließen | Bank | alle ~15–20 min | Assistent | Quartal |
| Dividende | CEO | ≤ 1× pro Quartal | 3 Taps | Firma → Verwalten |
| Firma gründen | Spieler | selten | Assistent (5 Schritte) | ＋ → „Firma gründen“ |
| Handelsangebot | Spieler | selten | Assistent | ＋ → „Handeln“ |
| Korrektur/Storno | Bank | selten | Assistent mit Begründung | Verlauf → Eintrag |

## 4. Navigation

### Spieler (Smartphone: Leiste unten)

| Bereich | Inhalt |
|---|---|
| **Start** | Konto, Vermögen, **offene Anfragen ganz oben**, Depot, eigene Firmen |
| **Börse** | alle Firmen mit Kurs und Veränderung, Marktplatz-Angebote, Firmenansicht |
| **＋** | Aktionsblatt: Miete zahlen, Miete fordern, Straße gekauft, Aktien kaufen/verkaufen, Handeln, Firma gründen, Bargeld ein-/auszahlen |
| **Brett** | Grundbuch nach Farbgruppen: wem gehört was, aktuelle Miete. Am Tisch die schnellste Antwort auf „Wem gehört das und was kostet es?“ |
| **Verlauf** | eigene Buchungen oder alle, jede mit „Warum?“ |

CEO-Funktionen bekommen **keinen eigenen Bereich**. Sie erscheinen als
„Verwalten“ in der Firmenansicht und als Karte auf der Startseite, nur beim CEO.
Die meisten Spieler sind keine CEOs; ein leerer Bereich würde nur verwirren.

### Bank (iPad: Seitenleiste)

**Eingang** (alles, was eine Entscheidung braucht) · **Spieler** · **Firmen** ·
**Brett** · **Quartal** · **Verlauf** · **Partie** (Code/QR, Pause, Einstellungen,
Beenden)

## 5. Responsives Verhalten

Das Layout richtet sich nach der **verfügbaren Breite**, nicht nach dem Gerätetyp.
Wichtig ist das fürs iPad: In Split View ist die App dort schmal und bekommt dann
automatisch das Handy-Layout.

| Breite | Typisch | Navigation | Inhalt | Aktionen öffnen als |
|---|---|---|---|---|
| < 600 px | Smartphone | Leiste unten | 1 Spalte | Bottom Sheet von unten |
| 600–1023 px | iPad hochkant, Split View | schmale Symbolleiste links | 1–2 Spalten | Bottom Sheet |
| ≥ 1024 px | iPad quer, Laptop | Seitenleiste mit Text | **Liste + Detail** nebeneinander | Panel rechts / Dialog |
| ≥ 1440 px | Desktop | Seitenleiste | zusätzlich Live-Verlauf als 3. Spalte | Dialog |

- Sichere Ränder (iPhone-Notch, Home-Balken) werden berücksichtigt.
- Ein Wechsel der Ausrichtung behält Ansicht und Eingaben.
- Jede Ansicht hat eine eigene Adresse. Nach dem Neuladen ist man wieder dort, wo
  man war; ein QR-Code kann direkt in den Beitritt führen.
- Smartphone quer wird unterstützt, aber nicht eigens optimiert.

## 6. Kernabläufe

### 6.1 Beitritt & Lobby *(S-01)*

```
┌───────────────────────────────┐
│ Partie beitreten              │
│                               │
│ Game-Code                     │
│ [A] [B] [C] [1] [2] [3]       │
│                               │
│ Nickname                      │
│ [ Patty               ]       │
│                               │
│ Spielfigur                    │
│ (Hut) (Auto) (Hund) (Schiff)  │
│                               │
│ [      Beitreten      ]       │
│                               │
│ oder QR-Code mit der Kamera   │
│ scannen                       │
└───────────────────────────────┘
```

- Der Code hat 6 große Felder; Großbuchstaben werden automatisch gesetzt,
  verwechselbare Zeichen gibt es nicht.
- Der QR-Code enthält den Link samt Code. Kamera drauf, und nur noch der Nickname
  fehlt.
- Danach wartet man in der **Lobby** („Warte auf die Bank …“), bis die Bank
  freigibt. Die Bank zeigt auf dem iPad Code und QR-Code groß zum Abscannen.

### 6.2 Firmenmiete, der häufigste Vorgang *(G-02)*

Es gibt zwei Wege zum selben Ergebnis:

- **A – Der Zahler meldet sich selbst** (schnellster Weg): ＋ → „Miete zahlen“ →
  Straße wählen → **Bezahlen**.
- **B – Jemand anderes fordert:** ＋ → „Miete fordern“ → Straße → Zahler (Figur
  antippen) → Senden. Beim Zahler öffnet sich die Forderung, und sie bleibt oben
  auf seiner Startseite, bis sie erledigt ist.

```
┌─────────────────────────────────┐
│ Miete zahlen                    │
│ Schlossallee  ·  TECH AG        │
├─────────────────────────────────┤
│ Kartenmiete (Wolkenkr.) 3.500 M │
│ Laden                  +  300 M │
├─────────────────────────────────┤
│ Gesamt                  3.800 M │
│                                 │
│ Dein Konto  8.450 → 4.650 M     │
│                                 │
│ [         Bezahlen          ]   │
│         Einspruch erheben       │
└─────────────────────────────────┘
```

- Bei Werken fragt die App zusätzlich die Augensumme ab (2–12).
- **Einspruch** landet im Eingang der Bank, die entscheidet.
- **Reicht das digitale Geld nicht**, zeigt die App den Fehlbetrag und den
  einfachsten Ausweg:

```
┌─────────────────────────────────┐
│ Miete zahlen            3.800 M │
├─────────────────────────────────┤
│ Digital verfügbar       2.600 M │
│ Es fehlen               1.200 M │
│                                 │
│ [ 1.200 M bar einzahlen und  ]  │
│ [        danach zahlen       ]  │
│                                 │
│ Weitere Möglichkeiten:          │
│ > Aktien verkaufen              │
│ > Ich kann nicht zahlen         │
└─────────────────────────────────┘
```

Mit „bar einzahlen und danach zahlen“ geht eine Anfrage an die Bank. Sobald die
Bank den Erhalt des Bargelds bestätigt, läuft die Miete automatisch durch. „Ich
kann nicht zahlen“ startet die Pleite-Abwicklung (§9).

### 6.3 Aktien kaufen *(A-02, A-03, A-04)*

```
┌────────────────────────────────┐
│ TECH AG kaufen                 │
├────────────────────────────────┤
│ Quelle                         │
│ (o) Reserve      5 St. à 112 M │
│ ( ) Max          5 St. à 118 M │
│                                │
│ Stückzahl    [ − ]   5  [ + ]  │
│              1 · 5 · max       │
├────────────────────────────────┤
│ Preis     5 × 112 M =   560 M  │
│ Danach   Konto        7.890 M  │
│          Anteil   30 % → 35 %  │
│                                │
│ Noch 16 Aktien, dann bist du   │
│ CEO (Max hat 50).              │
│                                │
│ [           Kaufen           ] │
└────────────────────────────────┘
```

- Quelle ist entweder die **Emissionsreserve** (zum Kurs; das Geld geht an die
  Firma) oder ein **Marktplatz-Angebot** (zum Angebotspreis; das Geld geht an den
  Verkäufer).
- Die App zeigt immer „**Danach**“, also den Kontostand und Anteil nach dem Kauf.
- Kontrolle wird sichtbar gemacht: „Noch 16 Aktien, dann bist du CEO.“
- Hat sich der Kurs inzwischen geändert, fragt die App nach („Kurs ist jetzt
  115 M – trotzdem kaufen?“).

### 6.4 Firma gründen (Assistent) *(U-01, U-02, A-02, G-07)*

1. **Farbgruppe wählen.** Auswählbar sind nur vollständige, hypothekenfreie
   Gruppen. Andere erscheinen ausgegraut mit Grund („Dir fehlt die Elisenstraße“).
2. **Startkapital:** mindestens 1.500 M, eingegeben über den Ziffernblock.
3. **Aktien behalten:** Schieberegler von 51 bis 100 (siehe unten).
4. **Name & Kürzel.**
5. **Zusammenfassung & Bezahlen:** 1.000 M Gebühr + Startkapital, die eingebrachten
   Straßen, danach die Wahl „digital bezahlen“ oder „**bar über die Bank**“.

```
┌───────────────────────────────┐
│ Firma gründen         3 / 5   │
├───────────────────────────────┤
│ Wie viele Aktien behältst du? │
│                               │
│ 51 |=========o------| 100     │
│            80 Aktien          │
│                               │
│ Startwert der Firma  2.300 M  │
│ Startkurs              29 M   │
│ Reserve: 20 Aktien, bringen   │
│ bis zu 580 M neues Kapital    │
│                               │
│ Je mehr du behältst, desto    │
│ mehr Kontrolle, aber desto    │
│ weniger Kapital von anderen.  │
│                               │
│ [ Zurück ]        [ Weiter ]  │
└───────────────────────────────┘
```

Danach öffnet sich die neue Firma mit dem Hinweis: „Lege die Besitzrechtkarten auf
die Firmenablage.“

### 6.5 Bank: Ein-/Auszahlung & Eingang

```
┌───────────────────┬────────────────────────────┐
│ Spieler           │ Patty    Digital 8.450 M   │
│───────────────────│────────────────────────────│
│ > Patty  8.450 M  │          1.250 M           │
│   Max    2.100 M  │                            │
│   Leo      640 M  │   [ 1 ] [ 2 ] [ 3 ]        │
│   Mia    5.300 M  │   [ 4 ] [ 5 ] [ 6 ]        │
│                   │   [ 7 ] [ 8 ] [ 9 ]        │
│                   │   [000] [ 0 ] [ < ]        │
│                   │                            │
│                   │   +100  +500  +1.000       │
│                   │                            │
│                   │ [Einzahlung] [Auszahlung]  │
└───────────────────┴────────────────────────────┘
```

Spieler antippen → Betrag (Ziffernblock + Schnellwerte) → **Einzahlung** oder
**Auszahlung**. Anfragen von Spielern (z. B. „bar einzahlen und zahlen“) landen
im Eingang und lassen sich mit einem Tap bestätigen:

```
┌─────────────┬──────────────────────┬────────────────────────────┐
│ BANK        │ Eingang              │ Leo: Einzahlung            │
│ ABC123      │──────────────────────│────────────────────────────│
│             │ > Leo                │ Bargeld erhalten?          │
│ > Eingang 3 │   Einzahlung 2.500 M │ 2.500 M für die Gründung   │
│ Spieler     │   (Gründung)         │ der NORD AG                │
│ Firmen      │                      │                            │
│ Brett       │   Max                │ Danach läuft die Gründung  │
│ Quartal     │   Einspruch Miete    │ automatisch durch.         │
│ Verlauf     │                      │                            │
│ Partie      │   Tom                │ [ Erhalten - buchen ]      │
│             │   möchte beitreten   │ [    Ablehnen       ]      │
│ * live      │                      │                            │
└─────────────┴──────────────────────┴────────────────────────────┘
```

### 6.6 Quartalsabschluss (Bank) *(G-04; Schritte hängen an R-01, R-05)*

1. **Start:** „Startspieler ist über Los gezogen“ → Quartal abschließen
2. **Ereigniswürfe** je Firma (physischer Würfel oder „App würfeln lassen“)
3. **Konjunktur-Wurf**
4. **Vorschau** des Quartalsberichts → **Abschließen**

```
┌───────────────────────────────┐
│ Quartal 3 abschließen  2 / 4  │
├───────────────────────────────┤
│ Ereigniswürfe (2 Würfel)      │
│                               │
│ TECH AG    Risiko hoch        │
│   Krise bei 2-4  Glück 11-12  │
│   Augensumme  [ 7 ]   ok      │
│                               │
│ RETAIL     Risiko niedrig     │
│   Krise bei 2    Glück 12     │
│   Augensumme  [   ]           │
│                               │
│ [ App würfeln lassen ]        │
│                               │
│ [ Zurück ]        [ Weiter ]  │
└───────────────────────────────┘
```

Nach dem Abschluss erscheint auf **allen** Geräten der Quartalsbericht als
Vollbild-Karten zum Durchwischen. Zuerst kommen Konjunktur und Firmen, am Ende eine
persönliche Karte („Dein Vermögen: +620 M“).

```
┌───────────────────────────────┐
│ Quartalsbericht Q3     2 / 5  │
├───────────────────────────────┤
│ TECH AG                       │
│ Kurs   100 M → 112 M  +12 %   │
│                               │
│ + Wolkenkratzer Schlossallee  │
│ + Mieteinnahmen 440 M         │
│ − Unterhalt 100 M             │
│   Ereignis: keines (7)        │
│                               │
│ Dein Depot: +360 M            │
│                               │
│    o  o  *  o  o              │
│    wischen für weiter         │
└───────────────────────────────┘
```

### 6.7 Firma verwalten (CEO)

Erreichbar über die Firmenansicht → **Verwalten**, nur für den CEO:
- **Kasse & Dividende:** „Maximal ausschüttbar: 1.240 M (begrenzt durch Reserve)“
  *(D-01)*
- **Straßen & Gebäude:** bauen und verkaufen nach den Box-Regeln *(U-04)*
- **Projekte & Slots** *(kommt mit v0.2, P-01 ff.)*
- **Reserve-Aktien anbieten:** Stückzahl festlegen
- **Anträge:** z. B. „Straße verkaufen“ braucht > 50 %; Aktionäre stimmen per Tap
  ab *(K-01)*
- **Zahlungsnot-Modus:** Ein roter Rahmen zeigt die geführte Liste der
  Notverkäufe *(R-04)*

### 6.8 Verlauf & „Warum?“

Der Verlauf ist eine Liste aus Symbol, Text, Betrag (±) und Uhrzeit, filterbar
nach **Ich / eine Firma / Alle**. Ein Eintrag lässt sich antippen und öffnet die
Erklärung:

```
┌───────────────────────────────┐
│ Warum? TECH AG, Quartal 3 → 4 │
├───────────────────────────────┤
│ Unternehmenswert              │
│  9.500 M  →  10.640 M         │
│                               │
│ + 800 M  Wolkenkratzer        │
│          Schlossallee:        │
│          Ertragskraft         │
│          +400 M/Q × 2         │
│ + 440 M  Mieteinnahmen        │
│ − 100 M  Unterhalt Fabrik     │
├───────────────────────────────┤
│ Aktienkurs  100 M → 112 M     │
│ Dein Depot  30 St. +360 M     │
│                               │
│ Fehler entdeckt?              │
│ > Bank um Korrektur bitten    │
└───────────────────────────────┘
```

„Bank um Korrektur bitten“ erzeugt eine Anfrage im Eingang der Bank. Spieler
können selbst nichts rückgängig machen; Korrekturen sind Gegenbuchungen der Bank
*(S-04)*.

## 7. Startseite und iPad-Ansicht

**Smartphone – Startseite:**

```
┌───────────────────────────────┐
│ Patty (Hut)       Q3  * live  │
├───────────────────────────────┤
│ Digitales Konto               │
│ 8.450 M                       │
│ Vermögen o. Bargeld 14.720 M  │
├───────────────────────────────┤
│ ! Miete an TECH AG            │
│   Schlossallee      3.800 M   │
│   [ Bezahlen ]  [Einspruch]   │
├───────────────────────────────┤
│ Depot                         │
│ TECH    30 St.  112 M +12 %   │
│ RETAIL  15 St.   87 M  −2 %   │
├───────────────────────────────┤
│ BAU AG  (du bist CEO)         │
│ Kasse 4.200 M   [Verwalten]   │
├───────────────────────────────┤
│ Start Börse  [+]  Brett Verl. │
└───────────────────────────────┘
```

**iPad quer – Börse mit Liste und Detail.** Dieselben Inhalte, aber
nebeneinander statt gestapelt:

```
┌───────────┬──────────────────────┬────────────────────────────────────────┐
│ Patty     │ Börse                │ TECH AG                      CEO: Max  │
│ 8.450 M   │──────────────────────│ Wert 10.640 M       Kurs 112 M  +12 %  │
│           │ TECH     112 M +12 % │────────────────────────────────────────│
│ Start     │ RETAIL    87 M  −2 % │ Kurs je Quartal  Q1 .:|||: Q4          │
│ > Börse   │ BAU AG    54 M   0 % │                                        │
│ Brett     │ HAFEN    203 M  +9 % │ Aktionäre   Max 50 %  Patty 30 %       │
│ Verlauf   │                      │             Leo 15 %  Reserve 5        │
│           │ Angebote (3)         │                                        │
│           │ Max: 5 TECH à 118    │ Straßen     Schlossallee  [###]        │
│           │                      │             Parkstraße    [#--]        │
│ [+]Aktion │                      │                                        │
│           │                      │ [Warum?]  [Kaufen]  [Handeln]          │
└───────────┴──────────────────────┴────────────────────────────────────────┘
```

## 8. Bedienmuster

| Muster | Regel |
|---|---|
| **Aktionsblatt** | Smartphone: Bottom Sheet von unten. iPad/Desktop: Panel rechts. Immer mit Zusammenfassung und „Danach“-Zustand |
| **Bestätigen** | Normale Aktion: ein Tap. **Ab 1.000 M und bei Unumkehrbarem** (Gründung, Notverkauf, Auflösung, Storno): **gedrückt halten** (ca. 1 s), damit nichts versehentlich passiert *(UI-02)* |
| **Beträge** | Eigener großer Ziffernblock mit `000` und Schnellwerten (+100, +500, +1.000), nie die Systemtastatur, die den halben Bildschirm verdeckt |
| **Spieler wählen** | Chips mit Spielfigur + Name *(UI-01)* |
| **Straße wählen** | Farbraster wie auf dem Brett, zuletzt benutzte oben |
| **Rückmeldung** | Geänderte Zahlen zählen sichtbar hoch/runter und leuchten kurz grün/rot, **immer mit Vorzeichen bzw. Pfeil**, nicht nur Farbe |
| **Warten** | Der Knopf zeigt „wird ausgeführt …“. Doppeltippen ist harmlos, weil der Server jede Aktion nur einmal ausführt |
| **Fehler** | In Klartext mit Ausweg: „Max hat inzwischen 3 der Aktien gekauft – noch 2 verfügbar.“ |
| **Erstes Mal** | Kurze Erklärung bei neuen Konzepten (Emissionsreserve, „Dividende senkt den Kurs“, „Ertragswert zählt ab Quartalsende“) |
| **Leere Zustände** | Erklären den nächsten Schritt: „Noch keine Firma. So gründest du eine …“ |

## 9. Benachrichtigungen & Sonderzustände

| Ereignis | Darstellung |
|---|---|
| Forderung an dich | Karte ganz oben auf Start + Sheet öffnet sich; bleibt, bis erledigt |
| Geld erhalten | kurzer Hinweis („+400 M Dividende von TECH“) |
| Kursänderung im Depot | gebündelt, nicht bei jeder Kleinigkeit |
| CEO-Wechsel, Abstimmung | Karte auf Start |
| Quartalsbericht | Vollbild auf allen Geräten |
| Partie pausiert | Banner oben; nur die Bank kann handeln |
| **Verbindung weg** | Status „verbinde …“; Inhalte bleiben sichtbar, aber grau mit „Stand 20:41“. Geld-Aktionen sind gesperrt |
| **Zahlungsnot** | Geführte Liste der Möglichkeiten: bar einzahlen, Aktien anbieten, Aktien-Notverkauf an die Bank (50 %), „Ich bin pleite“ → Bank wickelt ab. Häuser verkaufen und Hypotheken laufen physisch am Brett |

**Technische Grenzen:** Safari auf dem iPhone kann nicht vibrieren, und
Push-Benachrichtigungen gehen dort nur, wenn die App zum Home-Bildschirm
hinzugefügt wurde. Version 1 setzt daher auf Hinweise **in der App**. Für das
Bank-iPad gibt es die Option „Bildschirm anlassen“.

## 10. Visuelle Sprache

- **Ruhig, Farbe nur mit Bedeutung.** Die Grundfläche ist neutral.
- **Farbgruppen** der Straßen dienen als Erkennungsfarbe, als Streifen wie auf
  der Besitzrechtkarte.
- **Firmen** haben eine eigene Farbe und ein Kürzel-Badge (TECH, BAU …).
- **Plus/Minus:** Grün/Rot, immer mit Vorzeichen und Pfeil, damit es auch bei
  Farbschwäche funktioniert.
- **Zahlen** mit gleich breiten Ziffern, damit sie beim Ändern nicht springen.
  Kontostände groß, deutsches Format „8.450 M“, echtes Minuszeichen „−“.
- **Hell- und Dunkelmodus.** Der Dunkelmodus ist bei Spieleabenden angenehm.
- **Eigene, neutrale Gestaltung**, keine Hasbro-Grafiken oder -Logos.
- **Barrierearm:** Kontrast nach WCAG AA, Tippflächen ≥ 44 px, Zoom und größere
  Schrift erlaubt, Beschriftungen für Screenreader.

## 11. Bausteine für die Umsetzung

App-Rahmen (Leiste/Seitenleiste + Verbindungsstatus) · Aktionsblatt (Sheet/Panel)
· Ziffernblock · Spieler-Auswahl · Straßen-Auswahl (Farbraster) · Firmen-Badge ·
Geldbetrag (formatiert, animiert) · Veränderung (±, Pfeil) · „Warum?“-Aufschlüsselung
· Gedrückt-halten-Knopf · Anfrage-Karte · Hinweis (Toast) · Assistent (Schritte)
· Mini-Kursverlauf

Technik wie in der Architektur: React, Tailwind, Radix-Bausteine, PWA. Ziel für die
erste Ladezeit über Mobilfunk: deutlich unter 200 KB JavaScript (komprimiert).

## 12. Offene UI-Fragen

| ID | Frage | Empfehlung |
|---|---|---|
| UI-01 | Spielfiguren als Avatare? | **Ja.** Beim Beitritt wählt man eine Figur (neutrale Symbole). Am Tisch erkennt man Spieler schneller an der Figur als am Namen |
| UI-02 | „Gedrückt halten“ bei großen Beträgen? | **Ja**, ab 1.000 M und bei allem Unumkehrbaren |
| UI-03 | Tischansicht (TV/iPad in der Mitte) schon in Version 1? | **Nein**, später. Den Quartalsbericht bekommen zunächst alle aufs eigene Gerät |
| UI-04 | Sprache | **Deutsch.** Alle Texte liegen zentral, damit Englisch später leicht nachrüstbar ist |
