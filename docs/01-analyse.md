# 01 – Konzeptanalyse

> Stand: erste Analyse. Gibt meine ehrliche Einschätzung wieder: was trägt,
> wo es Widersprüche gibt, welche Exploits ich sehe und was das Balancing
> bestimmt. Konkrete Regelvorschläge mit Entscheidungs-IDs stehen in
> [`02-entscheidungen.md`](02-entscheidungen.md).

---

## 1. Gesamteindruck

Das Konzept ist stark, weil es eine **klare Trennung** hat:

| Ebene | Wo | Wer rechnet |
|---|---|---|
| Würfeln, Ziehen, Kaufen, normale Miete | Brett (physisch) | Spieler |
| Unternehmen, Aktien, Bewertung, Projekte, Dividenden, Ereignisse | App (digital) | Server |

Diese Trennung sollten wir konsequent verteidigen. Je mehr Brettgeschehen in die
App eingetippt werden muss, desto mehr bremst die App das Spiel. Die Leitfrage
für jede Regel lautet deshalb: **Wie viele Taps kostet das am Tisch?**

Was mir besonders gut gefällt:
- **Keine neuen Aktien und keine Kredite.** Das schließt die beiden häufigsten
  Ursachen für unendliches Geld in Wirtschaftsspielen von vornherein aus.
- **Miete zahlt immer der Spieler persönlich.** Unternehmen bleiben dadurch reine
  Vermögensträger und werden keine Schutzschilde.
- **Seltene große Ereignisse statt Dauerkosten.** Spielt sich viel besser als
  ständiges Kleinvieh-Abbuchen.

---

## 2. Drei strukturelle Probleme

Diese drei Punkte müssen wir lösen, bevor Details sinnvoll sind.

### 2.1 Wie kommt ein Unternehmen an das Geld anderer Spieler?

**Widerspruch:** In der Unternehmer-Strategie steht „verdient durch … Kapital
anderer Spieler“. Gleichzeitig gilt: keine neuen Aktien, Aktien wechseln nur den
Besitzer.

Wenn der Gründer alle Aktien bekommt und Max ihm 20 Aktien abkauft, landet Max'
Geld **beim Gründer privat**, nicht in der Firma. Das Unternehmen selbst könnte
also nie Kapital von Investoren einsammeln. Wachstum ginge nur aus eigenen
Mieteinnahmen.

**Vorschlag: Emissionsreserve (Börsengang bei der Gründung).**
- Die Aktienanzahl wird bei der Gründung **einmalig und endgültig** festgelegt
  (z. B. 100 Aktien).
- Der Gründer erhält einen Teil davon (z. B. mindestens 51). Den Rest hält das
  Unternehmen als **Emissionsreserve**.
- Das Unternehmen kann Reserve-Aktien zum aktuellen Kurs verkaufen. Der Erlös geht
  **in die Firmenkasse**.
- Reserve-Aktien haben kein Stimmrecht, bekommen keine Dividende und zählen nicht
  bei der Kursberechnung (Kurs = Wert / **umlaufende** Aktien).

Damit bleibt „niemals neue Aktien“ wahr: Es existieren von Anfang an genau 100
Stück. Verkäufe aus der Reserve zum Kurs sind für die übrigen Aktionäre
wertneutral: Die Kasse wächst genau um den Wert der neu umlaufenden Aktien. Den
Rechenweg zeigt [`02-entscheidungen.md` → A-02](02-entscheidungen.md#a-02).

→ Entscheidung **A-02**

### 2.2 Zwei Geldwelten: physisch und digital

Es gibt Papiergeld (Brett) und digitales Geld (App). Daraus folgen Fragen, die
das Konzept noch nicht beantwortet:

1. **Miete auf Unternehmensimmobilien** muss digital fließen, denn eine Firma hat
   kein Papiergeld. Wer nur Papiergeld hat, muss vorher einzahlen. Wie oft
   passiert das am Tisch, und wird die Bank zum Flaschenhals?
2. **Gesamtvermögen**: Die App kennt das Papiergeld nicht. Die Anzeige
   „Gesamtvermögen 14.720 M“ wäre also unvollständig, solange niemand sein Bargeld
   einträgt.
3. **Privatimmobilien**: Damit die App eine Gründung prüfen („vollständige
   Farbgruppe“) und ein Vermögen anzeigen kann, muss sie wissen, wem welche Straße
   gehört. Gekauft wird aber physisch.

**Vorschlag:** Die App führt ein **Grundbuch** für alle Straßen. Ein Kauf am Brett
ist ein Tap („Ich habe die Badstraße gekauft“), den alle sehen und den die Bank
korrigieren kann. Geld bleibt hybrid: Das Brett läuft mit Papiergeld, die
Wirtschaftsebene digital. Das Datenmodell erlaubt später zusätzlich einen
**Volldigital-Modus** ohne Papiergeld.

→ Entscheidungen **G-02, G-03**

### 2.3 Die App kennt keine Runden

Projekterträge, laufende Kosten, Ereignisse, Dividendentermine und
Kursentwicklung brauchen einen **Takt**. Das Brett hat zwar Runden, die App sieht
davon aber nichts.

**Vorschlag: Quartal.** Ein Quartal endet, wenn der Startspieler über Los zieht.
Die Bank tippt dann „Quartal abschließen“, oder der Startspieler tut es selbst.
Beim Quartalsabschluss passiert alles Periodische gebündelt und wird als kurzer
**Quartalsbericht** angezeigt. Das passt zum Thema (Börse, Quartalszahlen) und
bündelt die Rechnerei auf wenige, klar erkennbare Momente.

→ Entscheidung **G-04**

---

## 3. Weitere Widersprüche und Lücken

| # | Beobachtung | Warum es ein Problem ist | Vorschlag / Entscheidung |
|---|---|---|---|
| W1 | Beispiel „Wolkenkratzer mit 3 Slots“, belegt mit Fabrik + 2 × Laden | Ist die Fabrik ein 2-Slot-Projekt, sind das 4 Slots | Slot-Größen festlegen → **P-02** |
| W2 | Projekt namens „Hotel“ | Kollidiert mit dem Monopoly-Hotel, Verwechslung am Tisch | z. B. „Grand Resort“ → **P-02** |
| W3 | Keine Kredite, Monopoly kennt aber **Hypotheken** | Eine Hypothek ist ein Bankkredit | Firmen dürfen nicht beleihen; eingebrachte Straßen müssen hypothekenfrei sein → **U-03** |
| W4 | „Kontrolle ab > 50 %“ | Wer führt die Firma, wenn niemand > 50 % hält? | CEO = größter Aktionär, Grundsatzfragen per Mehrheit → **K-01** |
| W5 | Kein Minus erlaubt, Ereignisse kosten aber Geld | Was passiert, wenn die Kasse nicht reicht, ohne dass eine Schuld entsteht? | Notverkaufsmodus mit fester Reihenfolge → **R-04** |
| W6 | Unternehmen haben keinen Zug am Brett | Wann dürfen sie bauen, und wie bekommen sie freie Straßen? | Bauen zwischen den Zügen; Straßen nur durch Handel → **U-04** |
| W7 | Die Bank kann Geld übertragen und korrigieren | Spielt der Banker mit, kann er sich selbst begünstigen | Vier-Augen-Prinzip bei Buchungen aufs eigene Konto → **S-02** |
| W8 | „Aktienkurs ergibt sich aus Unternehmensentwicklung“, Spieler handeln aber zu frei verhandelten Preisen | Bewegen Handelspreise den Kurs, wird er manipulierbar | Kurs rein fundamental; Handelspreise in einem Preisband → **A-03, A-04** |
| W9 | Ein Spieler, der Aktien hält, geht bankrott | Monopoly regelt nur Straßen und Geld | Aktien gehen an den Gläubiger → **K-03** |
| W10 | Spielende | Klassisch „alle bis auf einen pleite“ kann mit Firmen sehr lange dauern | Optional Zeit-/Quartalslimit mit Vermögenswertung → **G-05** |
| W11 | Dynamische Mieten von 5.000 M und mehr | Können Spieler mit einem einzigen Wurf aus dem Spiel nehmen | Bewusst so wollen oder Mietdeckel → **P-04** |

---

## 4. Gefundene Exploits

Jeder Exploit hat eine Gegenmaßnahme, die in den Entscheidungen verankert ist.

| # | Exploit | Wie er funktioniert | Gegenmaßnahme |
|---|---|---|---|
| X1 | **Gründen & Abstoßen** | Kauft die Bank Aktien immer zum Kurs an und enthält der Kurs schon einen Ertragsaufschlag, ist Gründen und sofort Verkaufen ein Gewinn aus dem Nichts | Kein automatischer Bank-Ankauf (**A-05**); Ertragswert erst nach dem ersten Quartal (**B-02**) |
| X2 | **Selbstbedienung (Insidergeschäft)** | CEO (51 %) verkauft seine private Badstraße (60 M) für 3.000 M an die eigene Firma. Die Minderheitsaktionäre zahlen 49 % davon | Preisband für Geschäfte zwischen Firma und Insidern, sonst Zustimmung der übrigen Aktionäre (**K-02**) |
| X3 | **Endspiel-Pumpen** | Kurz vor Spielende Projekte bauen, damit der Ertragsaufschlag das Vermögen auf dem Papier aufbläht | Ertragswert wird nur beim Quartalsabschluss festgestellt; das Spielende ist kein Quartalsabschluss (**B-02**) |
| X4 | **Verdeckte Schenkung / Königsmacher** | Ein unterlegener Spieler kauft einem Freund 1 Aktie für 5.000 M ab | Preisband für Aktienhandel (**A-04**) |
| X5 | **Kursmanipulation durch Scheingeschäfte** | Zwei Spieler handeln untereinander zu Fantasiepreisen, um den Kurs zu bewegen | Kurs hängt nicht von Handelspreisen ab (**A-03**) |
| X6 | **Ausplündern per Dividende** | Gesamte Kasse ausschütten, danach ist die Firma handlungsunfähig | Ausschüttung nur aus Gewinnen und oberhalb einer Mindestreserve (**D-01**) |
| X7 | **Zirkuläre Beteiligungen** | A hält B, B hält A: Werte blähen sich gegenseitig auf | Beteiligungsgraph muss azyklisch bleiben, Prüfung bei jedem Kauf (**K-04**) |
| X8 | **Falsche Mietforderung** | Ein CEO behauptet, Max sei auf seiner Straße gelandet | Der Zahler bestätigt mit einem Tap; bei Streit entscheidet die Bank; alles protokolliert (**G-02**) |
| X9 | **Doppelte Ausführung** | Doppeltipp oder Netzwerk-Wiederholung kauft zweimal | Jeder Befehl trägt eine eindeutige ID, der Server führt ihn höchstens einmal aus (technisch) |
| X10 | **Wettlauf um die letzten Aktien** | Zwei Spieler kaufen gleichzeitig die letzten 5 Reserve-Aktien | Befehle pro Partie strikt nacheinander verarbeiten (technisch) |
| X11 | **Banker bucht sich selbst Geld** | Der Banker spielt mit und „korrigiert“ das eigene Konto | Vier-Augen-Prinzip, Bank-Aktionen für alle sichtbar (**S-02**) |
| X12 | **Fremder tritt bei** | Jemand kennt den Code und tritt als „Bank“ bei | Lobby-Freigabe durch die Bank, reservierte Namen, Rate-Limit (**S-01**) |
| X13 | **Vermögen vor Bankrott verstecken** | Kurz vor der Pleite Straßen billig an die Firma eines Freundes | Preisband (X2) gilt für alle Firmengeschäfte mit Straßen |
| X14 | **Schulden durch die Hintertür** | Offene Rechnungen sammeln statt zahlen | Zahlungspflichten werden sofort fällig; bis zur Begleichung ist die Firma gesperrt (**R-04**) |
| X15 | **Firmenmiete bar zahlen** | Mit Papiergeld zahlen, das die App nie sieht | Miete auf Firmenimmobilien nur digital (**G-02**) |

**Kein Exploit, aber wichtig zu erklären:** Wer Aktien kurz vor einer Dividende
kauft und danach verkauft, gewinnt nichts. Die Dividende senkt die Firmenkasse und
damit den Kurs um genau den ausgeschütteten Betrag. Die App sollte das beim ersten
Mal kurz erklären, damit es nicht als Fehler wirkt.

---

## 5. Balancing: die zentrale Frage

> **Warum sollte ich eine Farbgruppe in ein Unternehmen einbringen, statt sie
> privat zu behalten?**

Ist die Antwort „immer“, gibt es keinen Privatinvestor mehr. Ist sie „nie“, gibt
es keinen Unternehmer. Die Gründung braucht also echte Vor- **und** Nachteile:

| Vorteile Unternehmen | Nachteile Unternehmen |
|---|---|
| Nur Firmen können **Projekte** bauen (höhere Mieten, feste Erträge) | Gründungskosten an die Bank (weg) |
| Kapital von Investoren über die **Emissionsreserve** | Startkapital ist gebunden und nicht mehr privat verfügbar |
| **Ertragswert**: Die Firma ist mehr wert als ihre Teile, das lässt sich über Aktien versilbern | Mieten fließen in die Firma, nicht direkt in die eigene Tasche |
| **Haftungsbeschränkung**: Geht die Firma pleite, bleibt das Privatvermögen unberührt | Seltene Krisen-Ereignisse treffen nur Firmen |
| Kontrolle über fremde Firmen per Beteiligung | Gewinne müssen mit Minderheitsaktionären geteilt werden |

Die drei Strategien brauchen jeweils eine eigene Ertragsquelle:

| Strategie | Ertrag kommt aus | Risiko |
|---|---|---|
| 🏠 Privatinvestor | Miete direkt, ohne Abzug | Keine Projekte, kein Ertragswert, normales Monopoly-Risiko |
| 📈 Aktieninvestor | Kursanstieg + Dividenden, Streuung über viele Firmen | Abhängig von fremden CEOs, Krisen treffen die Kurse |
| 🏢 Unternehmer | Wertsteigerung durch Projekte, Verkauf von Anteilen, Kontrolle | Hohe Bindung, Krisen, Insolvenz |

### Folgerungen fürs Balancing
1. **Zahlen per Simulation festlegen, nicht nach Gefühl.** Die Spiellogik wird als
   reiner Rechenkern gebaut (siehe Architektur). Damit können wir tausende
   simulierte Partien durchrechnen und z. B. sehen, ob ein Laden sich nach 3 oder
   nach 12 Quartalen amortisiert.
2. **Geldmenge im Blick behalten.** Geld entsteht bei der Bank (Los-Geld,
   Projekterträge) und verschwindet dorthin (Gebühren, Baukosten, Ereignisse).
   Erzeugen Projekterträge mehr Geld, als Kosten vernichten, gibt es Inflation und
   das Spiel endet nie.
3. **Mietexplosion begrenzen oder bewusst wollen** (W11). Mega-Edition-Mieten
   sind schon hoch; Projekte obendrauf beenden Partien schnell. Das kann Absicht
   sein, sollte aber eine bewusste Entscheidung sein.
4. **Erst einfach, dann reicher.** Ich empfehle, mit wenigen Projekttypen und
   wenigen Ereignissen zu starten und nach den ersten Testpartien zu erweitern.

---

## 6. Das Gesamtmodell auf einen Blick

```
                 ┌──────────────── Brett (physisch) ────────────────┐
                 │ Würfeln · Ziehen · Straßen kaufen · normale Miete │
                 └───────┬────────────────────────────┬─────────────┘
                 Grundbuch-Tap                Landung auf Firmenstraße
                         ▼                            ▼
┌─────────────────────────── App (digital) ───────────────────────────┐
│  Spielerkonten ⇄ Bank (Ein-/Auszahlung)                              │
│        │                                                             │
│        ├─ Gründung ─▶ Unternehmen ◀─ Miete (digital, aufgeschlüsselt)│
│        │              │  Kasse · Straßen · Gebäude · Projekte        │
│        │              │  Beteiligungen (azyklisch)                   │
│        ◀─ Dividende ──┤                                              │
│        ⇄ Aktienhandel ┤  Emissionsreserve → Kapital für die Firma    │
│                       ▼                                              │
│            Unternehmenswert = Substanzwert + Ertragswert             │
│            Aktienkurs = Wert / umlaufende Aktien                     │
│                                                                      │
│  Quartalsabschluss (Startspieler über Los):                          │
│   Projekterträge · Unterhalt · Ereignisse · Konjunktur ·             │
│   Ertragswert feststellen · Dividendenfenster · Quartalsbericht      │
└──────────────────────────────────────────────────────────────────────┘
```
