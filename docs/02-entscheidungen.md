# 02 – Offene Designentscheidungen

> Jede Entscheidung hat eine ID. Antworte einfach z. B. mit
> „A-01: einverstanden, G-05: lieber Zeitlimit“.
> Alle Zahlen sind **Startwerte für Simulation und Testpartien**, keine
> endgültigen Werte.

**Priorität**
- 🔴 blockiert das Datenmodell und wird zuerst gebraucht
- 🟡 blockiert das Regelwerk
- 🟢 kann später entschieden werden

**Status**
- ✅ entschieden
- ✅❓ entschieden, aber eine Rückfrage ist offen
- ⬜ offen; Text = meine Empfehlung

## Übersicht

| ID | Thema | Prio | Status | Entscheidung bzw. Empfehlung (kurz) |
|---|---|---|---|---|
| [G-01](#g-01) | Spielausgabe & Kartendaten | 🔴 | ✅❓ | Mega Black Edition, Startgeld 1.500 M, Los 200 M (beides bar); Kartendaten fehlen noch |
| [G-02](#g-02) | Was läuft über die App, was bleibt physisch? | 🔴 | ⬜ | Grundbuch in der App; Firmenmiete digital, Rest hybrid |
| [G-03](#g-03) | Bargeld & Gesamtvermögen | 🟢 | ⬜ | Vermögen „ohne Bargeld“ anzeigen (durch G-05 weniger wichtig) |
| [G-04](#g-04) | Takt der Wirtschaft | 🔴 | ✅ | Quartal endet, wenn der Startspieler über Los zieht |
| [G-05](#g-05) | Spielende & Wertung | 🟡 | ✅ | Klassisch: Die Partie endet durch Pleite |
| [G-06](#g-06) | Sichtbarkeit von Kontoständen | 🟡 | ⬜ | Alles öffentlich |
| [G-07](#g-07) | Digitales Startguthaben | 🟡 | ⬜ | 0 M; das Startgeld ist komplett Bargeld |
| [U-01](#u-01) | Gründungsvoraussetzung | 🔴 | ✅ | Vollständige Farbgruppe wird in die Firma eingebracht |
| [U-02](#u-02) | Gründungskosten & Startkapital | 🔴 | ✅❓ | Gebühr 1.000 M an die Bank, Startkapital 1.500 M in die Firma |
| [U-03](#u-03) | Hypotheken | 🟡 | ⬜ | Firmen beleihen nie; Straßen müssen hypothekenfrei sein |
| [U-04](#u-04) | Bauen & Straßenerwerb durch Firmen | 🟡 | ⬜ | Bauen zwischen den Zügen; Straßen nur per Handel (+ ggf. Auktion) |
| [U-05](#u-05) | Mehrere Firmen / Zuschüsse | 🟢 | ⬜ | Unbegrenzt; Zuschüsse erlaubt |
| [A-01](#a-01) | Aktienanzahl | 🔴 | ✅ | 100 Aktien je Firma (1 Aktie = 1 %) |
| [A-02](#a-02) | Emissionsreserve | 🔴 | ✅ | Gründer ≥ 51 Aktien, Rest verkauft die Firma zum Kurs |
| [A-03](#a-03) | Kursbildung | 🔴 | ⬜ | Kurs = Wert / umlaufende Aktien, unabhängig von Handelspreisen |
| [A-04](#a-04) | Aktienhandel zwischen Spielern | 🟡 | ⬜ | Marktplatz-Angebote + Handelsangebote, Preisband 50–200 % |
| [A-05](#a-05) | Bank als Marktmacher | 🟡 | ⬜ | Nein, mit Ausnahme der Zahlungsnot (A-06) |
| [A-06](#a-06) | Notverkauf von Aktien an die Bank | 🔴 | ⬜ | Nur in Zahlungsnot, zu 50 % des Kurses, Aktien gehen in den Bankbestand |
| [B-01](#b-01) | Substanzwert | 🔴 | ⬜ | Kasse + Straßen + Gebäude + Projekte + Beteiligungen |
| [B-02](#b-02) | Ertragswert | 🔴 | ⬜ | Ertragskraft/Quartal × 2 × Konjunktur, festgestellt je Quartal |
| [D-01](#d-01) | Dividendenregel | 🟡 | ⬜ | Nur aus Gewinn, Kasse bleibt ≥ Reserve, 1× pro Quartal |
| [K-01](#k-01) | CEO & Kontrolle | 🔴 | ✅❓ | CEO = größter Aktionär; Verkauf nur mit > 50 %, außer zur Abwendung der Pleite |
| [K-02](#k-02) | Insidergeschäfte | 🟡 | ⬜ | Preisband 80–120 % oder Zustimmung der übrigen Aktionäre |
| [K-03](#k-03) | Aktien bei Spielerbankrott | 🔴 | ⬜ | An den Gläubiger; ist das die Bank, gehen sie in den Bankbestand (A-06) |
| [K-04](#k-04) | Beteiligungen zwischen Firmen | 🟢 | ⬜ | Erlaubt, azyklisch, aber erst Version 2 |
| [P-01](#p-01) | Projekt-Slots | 🟡 | Hotel = 1 Slot, Wolkenkratzer = 3 Slots |
| [P-02](#p-02) | Projektkatalog | 🟡 | 6 Projekte in zwei Familien (Miete / fester Ertrag) |
| [P-03](#p-03) | Bauzeit, Abriss, Verkauf | 🟡 | Fertig zum nächsten Quartal; Abriss bringt 50 % |
| [P-04](#p-04) | Mietdeckel | 🟢 | Erst kein Deckel, aber als Parameter vorbereiten |
| [R-01](#r-01) | Ereignisse auslösen | 🟡 | Beim Quartalsabschluss, physischer Würfel je Firma |
| [R-02](#r-02) | Risikostufe | 🟡 | Aus Projekt-Risikopunkten; bestimmt die Unglückszahlen |
| [R-03](#r-03) | Ereigniskatalog | 🟢 | Klein starten (6–8 Karten), später erweitern |
| [R-04](#r-04) | Zahlungsunfähigkeit & Insolvenz | 🟡 | Notverkaufsmodus, sonst Auflösung |
| [R-05](#r-05) | Konjunktur | 🟢 | 5 Stufen, wirkt auf den Ertragswert |
| [S-01](#s-01) | Beitritt | 🔴 | Code + Nickname + Freigabe durch die Bank, QR-Code |
| [S-02](#s-02) | Bank als Mitspieler | 🔴 | Getrennte Identitäten, Vier-Augen-Prinzip |
| [S-03](#s-03) | Gerätewechsel | 🟡 | Wiederbeitritts-Code über die Bank |
| [S-04](#s-04) | Korrekturen | 🟡 | Nur Gegenbuchungen mit Begründung, nie Löschen |
| [S-05](#s-05) | Accounts | 🟢 | Bank mit Login; Spieler-Accounts später optional |

---

## G – Grundlagen

<a id="g-01"></a>
### G-01 – Spielausgabe & Kartendaten 🔴 ✅❓
**Entschieden:** **Monopoly Mega Black Edition.** Startgeld 1.500 M, Los-Geld 200 M,
beides läuft **bar**. Das Währungssymbol ist in der App einstellbar (Standard: M).
**Noch offen:** die Kartendaten (siehe unten). Am einfachsten sind Fotos aller
Besitzrechtkarten (Vorderseiten) plus der Regelseiten zu Wolkenkratzern und
Bahnhöfen/Depots.

**Ursprüngliche Frage:** Welche Ausgabe genau?
Die App braucht für jede Straße: Name, Farbgruppe, Kaufpreis, Hauspreis,
Mietstaffel (unbebaut, 1–4 Häuser, Hotel, Wolkenkratzer), Hypothekenwert sowie die
Regeln für Bahnhöfe/Depots und Werke. Außerdem: Startgeld, Los-Geld, Anzahl der
Felder.

**Vorschlag:** Ich lege eine Datei (`board.json`) als Vorlage an, und du ergänzt die
Werte von den Besitzrechtkarten (oder schickst Fotos). Die Spielregeln selbst
bleiben die der Box; die App rechnet nur dort, wo Firmen im Spiel sind.

<a id="g-02"></a>
### G-02 – Was läuft über die App, was bleibt physisch? 🔴
| Vorgang | Vorschlag |
|---|---|
| Würfeln, Ziehen, Karten | physisch |
| Straße kaufen (privat) | physisch bezahlen + **1 Tap im Grundbuch** („gekauft“) |
| Miete auf **Privatstraße** | physisch (wie gewohnt) |
| Miete auf **Firmenstraße** | **digital**: Forderung stellen → Zahler tippt „Bezahlen“ |
| Los-Geld, Steuern, Karten | physisch |
| Ein-/Auszahlung digital ⇄ Bargeld | über die Bank |
| Alles mit Firmen und Aktien | digital |

Eine **Mietforderung** kann jeder Spieler stellen (meist der CEO oder der Zahler
selbst). Die App berechnet den Betrag samt Aufschlüsselung. Der Zahler bestätigt
mit einem Tap; bei Streit entscheidet die Bank. Reicht das digitale Guthaben
nicht, zahlt der Spieler zuerst Bargeld ein; geht das nicht, gelten die normalen
Monopoly-Regeln zum Bankrott. Bei Werken fragt die App die Augensumme ab.

**Alternative:** Ein Volldigital-Modus ohne Papiergeld (wie „Banking“-Editionen).
Ich würde ihn als **spätere Option** vorsehen, nicht als Standard.

<a id="g-03"></a>
### G-03 – Bargeld & Gesamtvermögen 🟡
Die App kennt dein Bargeld nicht. Vorschlag:
- Während der Partie zeigt sie „**Vermögen (ohne Bargeld)**“ = digitales Geld +
  Straßen + Gebäude + Aktien zum Kurs − Hypotheken.
- Bei der Schlusswertung trägt jeder sein Bargeld ein, die Bank bestätigt.
- Optional kann jeder sein Bargeld jederzeit freiwillig eintragen.

<a id="g-04"></a>
### G-04 – Takt der Wirtschaft (Quartal) 🔴 ✅
**Entschieden** wie vorgeschlagen. (Welche Schritte der Abschluss enthält, hängt
noch an den offenen Punkten B-02, P-03, R-01 und R-05.)

Ein **Quartal endet, wenn der Startspieler über Los zieht.** Die Bank
oder der Startspieler tippt „Quartal abschließen“.

Beim **Quartalsabschluss** passiert in fester Reihenfolge:
1. Feste Projekterträge gutschreiben, Unterhalt abbuchen
2. Ereignisse je Firma (siehe R-01)
3. Konjunktur aktualisieren (R-05)
4. Ertragswert neu feststellen (B-02)
5. Projekte im Bau → in Betrieb (P-03)
6. Quartalsbericht an alle: Was hat sich bei welcher Firma warum verändert?

**Alternative:** zeitbasiert (z. B. alle 15 Minuten). Davon rate ich ab, weil Pausen
und Spieltempo nicht dazu passen.

<a id="g-05"></a>
### G-05 – Spielende & Wertung 🟡 ✅
**Entschieden: (a) klassisch.** Die Partie endet, wenn alle bis auf einen Spieler
pleite sind.

**Folgen dieser Entscheidung:**
- Eine Schlusswertung ist nicht nötig. Exploit X3 (Endspiel-Pumpen) spielt damit
  kaum noch eine Rolle.
- Die Pleite-Regeln müssen jetzt **Aktien** abdecken: Wer hauptsächlich Aktien
  besitzt, braucht im Notfall einen Käufer → neue Entscheidung **A-06**, und K-03
  wird dringender.
- **Geldmenge im Blick behalten:** Erzeugen Ertragsprojekte und Dividenden mehr
  Geld, als Mieten und Kosten vernichten, geht niemand mehr pleite und die Partie
  endet nie. Das prüfen wir mit der Simulation.
- Später denkbar, aber **keine Regel**: Bei „Partie abbrechen“ zeigt die App eine
  Vermögensrangliste an.

**Damalige Optionen:**
- **(a) Klassisch:** bis nur noch einer übrig ist. Mit Firmen kann das sehr lange
  dauern.
- **(b) Quartalslimit (empfohlen als Standard):** Nach z. B. 8 Quartalen endet die
  Partie. Gewinner ist, wer das höchste Gesamtvermögen hat.
- **(c) Zeitlimit:** wie (b), aber nach Uhrzeit.

**Schlusswertung:** Bargeld + digitales Geld + Straßen (Kaufpreis) + Gebäude
(Baupreis) + Aktien zum Kurs − Hypotheken. Wichtig: Das Spielende ist **kein**
Quartalsabschluss. Was im letzten Quartal gebaut wurde, zählt nur mit den
Baukosten (verhindert Exploit X3).

<a id="g-06"></a>
### G-06 – Sichtbarkeit von Kontoständen 🟡
**Empfehlung:** Alles ist für alle sichtbar: Konten, Aktienbesitz, Firmenkassen.
- Bei Aktien ist Transparenz ohnehin nötig (Aktionärsliste, Kontrolle).
- Die Bank hat dadurch keinen Informationsvorteil.
- Es ist technisch einfacher: Alle Geräte bekommen denselben Spielstand.

**Alternative:** Private Kontostände sieht nur der Besitzer. Das ist möglich,
macht die Bank aber zum Informationsträger (siehe Fairness).

<a id="g-07"></a>
### G-07 – Digitales Startguthaben 🟡 ⬜
*Neu, folgt aus G-01.*
Das Startgeld von 1.500 M ist Bargeld. **Vorschlag:** Digitale Konten starten mit
**0 M**. Digitales Geld entsteht nur durch Einzahlung, Firmenmiete, Dividenden und
Aktienverkäufe.

**Folge für die Bedienung:** Die Gründung kostet 2.500 M digital (U-02). Damit
dafür nicht zwei Schritte nötig sind, bietet die App „**Gründen mit
Bareinzahlung**“ an: Der Gründer gibt der Bank das Bargeld, die Bank tippt
„erhalten“, und die Gründung läuft in einem Zug durch.

---

## U – Unternehmen

<a id="u-01"></a>
### U-01 – Gründungsvoraussetzung 🔴 ✅
**Entschieden** wie vorgeschlagen.
- Der Gründer besitzt eine **vollständige Farbgruppe** privat, alle Straßen
  hypothekenfrei.
- Er **bringt die Gruppe samt Gebäuden in die Firma ein**. Die Besitzrechtkarten
  wandern auf eine Firmenkarte bzw. Firmenablage am Tisch.

**Warum einbringen?** Bliebe die Gruppe privat und wäre nur Voraussetzung, besäße
die Firma außer Geld nichts. Die Gruppe ist der natürliche Kern des Unternehmens.

**Später denkbar:** eine „Verkehrs-AG“ aus allen Bahnhöfen oder eine
„Versorger-AG“ aus beiden Werken.

<a id="u-02"></a>
### U-02 – Gründungskosten & Startkapital 🔴 ✅❓
**Entschieden:** feste Beträge für jede Farbgruppe:
- **Gründungsgebühr** an die Bank: **1.000 M**
- **Startkapital** in die Firmenkasse: **1.500 M**

**Rückfrage:** Sind 1.500 M fest oder ein **Minimum**? Ich würde mehr erlauben:
Wer mehr Kapital mitbringt, kann schneller Projekte bauen, und seine Aktien sind
entsprechend mehr wert. Für die anderen Spieler ist das neutral.

**Beispiel:** Eine unbebaute Gruppe mit zusammen 800 M Kaufpreis.
- Der Gründer zahlt 2.500 M (1.000 M an die Bank, 1.500 M in die Firma) und
  bringt die Straßen ein.
- Startwert der Firma: 1.500 (Kasse) + 800 (Straßen) = **2.300 M**
- Behält er 60 Aktien: Kurs = 2.300 / 60 ≈ **38 M**. Die 40 Reserve-Aktien können
  der Firma bis zu ~1.520 M frisches Kapital bringen.

**Was das fürs Balancing bedeutet** (kein Einwand, nur zur Einordnung):
- 2.500 M sind mehr als das gesamte Startgeld. Gründen wird damit ein Zug fürs
  **mittlere Spiel**, also nicht zu billig, wie gewünscht.
- Die Gebühr von 1.000 M ist weg. Rechnerisch lohnt sich eine Gründung, sobald
  der Ertragswert (B-02) über 1.000 M liegt. Das erreichen vor allem **bebaute**
  Gruppen. Unbebaute günstige Gruppen (z. B. Badstraße) werden selten gegründet,
  denn die feste Gebühr trifft sie relativ am stärksten. Ob das so bleiben soll,
  zeigt die Simulation.

<a id="u-03"></a>
### U-03 – Hypotheken 🟡
Eine Hypothek ist ein Bankkredit. **Firmen dürfen daher nie beleihen.** Straßen, die
in eine Firma eingebracht oder an sie verkauft werden, müssen hypothekenfrei sein.
Privatspieler dürfen weiterhin nach normalen Regeln beleihen.

<a id="u-04"></a>
### U-04 – Bauen & Straßenerwerb durch Firmen 🟡
- **Bauen:** Der CEO darf zwischen den Spielzügen bauen, nach den normalen
  Bauregeln (gleichmäßig bauen, Gebäudevorrat der Box). Bezahlt wird aus der
  Firmenkasse; die Figuren stellt er aufs Brett.
- **Straßen erwerben:** Firmen landen nie auf einem Feld und können daher nicht
  direkt von der Bank kaufen. Erwerb nur **per Handel** mit Spielern oder anderen
  Firmen.
- **Option:** Firmen dürfen bei Monopoly-Versteigerungen mitbieten (der CEO bietet
  für die Firma). Das macht Firmen aktiver, ohne die Grundregeln zu brechen.

<a id="u-05"></a>
### U-05 – Mehrere Firmen, Zuschüsse, Namen 🟢
- Ein Spieler darf mehrere Firmen gründen (je eine Farbgruppe). Eine Firma darf
  per Handel mehrere Gruppen besitzen.
- **Zuschuss:** Jeder Aktionär darf Privatgeld in die Firma einzahlen, ohne neue
  Aktien dafür zu bekommen (z. B. als Rettung vor der Insolvenz). Ein Zuschuss gilt
  nicht als Gewinn und kann deshalb nicht als Dividende zurückfließen.
- Name + Kürzel (3–4 Buchstaben, eindeutig); die Bank kann umbenennen.

---

## A – Aktien

<a id="a-01"></a>
### A-01 – Aktienanzahl 🔴 ✅
**Entschieden: 100 Aktien je Firma.**
- 1 Aktie = 1 %, das lässt sich am Tisch sofort im Kopf rechnen.
- Kurse sind ganze M-Beträge, wie bei Monopoly-Geld (keine Cent-Beträge).
- Mehr Stückelung braucht eine Partie mit 4–8 Spielern nicht.

**Alternative:** 1.000 Aktien wie in deinem Beispiel (Kurs 18,40 M). Feiner, aber
mit Nachkommastellen und unhandlichen Prozenten (z. B. 3,7 %).

<a id="a-02"></a>
### A-02 – Emissionsreserve 🔴 ✅
**Entschieden** wie vorgeschlagen.

Löst das Problem „Wie kommt die Firma an Investorengeld?“ (Analyse 2.1).
- Bei der Gründung entstehen **einmalig** 100 Aktien. Danach nie wieder welche.
- Der Gründer wählt, wie viele er behält (**mindestens 51**). Den Rest hält die
  Firma als **Emissionsreserve**.
- Der CEO legt fest, wie viele Reserve-Aktien zum Kauf angeboten werden. Jeder
  Spieler kann sie sofort zum Kurs kaufen; das Geld geht in die Firmenkasse.
- Reserve-Aktien: kein Stimmrecht, keine Dividende, zählen nicht zu den
  umlaufenden Aktien.

**Rechenbeispiel (wertneutral):** Die Firma ist 6.000 M wert. Der Gründer hält 60
Aktien, 40 liegen in der Reserve. Kurs = 6.000 / 60 = **100 M**.
Max kauft 10 Reserve-Aktien für 1.000 M. Danach: Wert 7.000 M, 70 umlaufende
Aktien, Kurs = **100 M**. Niemand wurde verwässert, die Firma hat 1.000 M mehr
Kapital.

<a id="a-03"></a>
### A-03 – Kursbildung 🔴
**Kurs = Unternehmenswert / umlaufende Aktien**, auf ganze M gerundet.

Der Kurs hängt **nicht** von Handelspreisen zwischen Spielern ab. Dadurch ist er
- vollständig erklärbar („Wert stieg um 800 M, weil …“),
- nicht manipulierbar (Exploits X4, X5),
- für alle gleich und sofort aktuell.

Die Spannung entsteht trotzdem: Wer früh erkennt, welche Firma wachsen wird, kauft
günstig. Spekuliert wird auf die Entwicklung der Firma, nicht auf Stimmungen.

<a id="a-04"></a>
### A-04 – Aktienhandel zwischen Spielern 🟡
Zwei Wege, beide nur mit **digitalem** Geld:
1. **Marktplatz:** Ein Spieler stellt X Aktien zum Preis P ein, jeder kann sofort
   kaufen. Am Tisch geht das schnell, weil niemand verhandeln muss.
2. **Handelsangebot:** ein Paket zwischen zwei Parteien (Aktien + Straßen + Geld in
   beliebiger Kombination), wie ein klassischer Monopoly-Deal. Die Gegenseite
   bestätigt, der Server führt das Paket ganz oder gar nicht aus.

**Preisband:** Aktien werden zu 50 %–200 % des aktuellen Kurses gehandelt. Das
lässt Verhandlungsspielraum und verhindert verdeckte Geldgeschenke.

<a id="a-05"></a>
### A-05 – Bank als Marktmacher 🟡
**Frage:** Soll die Bank jederzeit Aktien zum Kurs ankaufen, damit man immer
verkaufen kann?

**Empfehlung: Nein.** Kauft die Bank zum Kurs und enthält der Kurs einen
Ertragsaufschlag, wird Gründen und Verkaufen zur Gelddruckmaschine (Exploit X1).
Liquidität kommt stattdessen aus der Emissionsreserve und vom Marktplatz.
Die einzige Ausnahme ist die Zahlungsnot, siehe **A-06**.

Ausdrücklich **nicht** vorgesehen: Leerverkäufe, Optionen, Aktienrückkäufe (diese
evtl. später).

<a id="a-06"></a>
### A-06 – Notverkauf von Aktien an die Bank 🔴 ⬜
*Neu. Folgt aus G-05 (Ende durch Pleite) zusammen mit A-05 (keine Bank als
Käufer).*

**Problem:** Bei Monopoly ist die Bank in der Not immer Käufer: Häuser nimmt sie
zum halben Preis zurück, Straßen beleiht sie zum Hypothekenwert. Für Aktien gäbe
es ohne eigene Regel **keinen** sicheren Käufer. Dann kann zweierlei passieren:
- Ein Spieler mit Aktien im Wert von 5.000 M, aber ohne Bargeld, geht wegen 300 M
  Miete pleite, weil gerade niemand seine Aktien kaufen will.
- Oder er bettelt am Tisch um einen Käufer, was Absprachen und Königsmacherei
  fördert.

**Vorschlag:**
- **Nur in Zahlungsnot** (eine Zahlung ist anders nicht möglich) darf ein Spieler
  oder eine Firma Aktien an die Bank verkaufen, zu **50 % des Kurses**. Das
  entspricht dem Hypothekenwert bei Straßen.
- Die Aktien kommen in einen **Bankbestand**: Die Bank bietet sie auf dem
  Marktplatz zum vollen Kurs an, und der Erlös geht an die Bank. Aktien im
  Bankbestand haben kein Stimmrecht, und ihre Dividende geht an die Bank.
- Am Kurs ändert das nichts, denn die Aktien bleiben im Umlauf.

**Warum kein Exploit:** Wer an die Bank verkauft, bekommt die Hälfte. Wer
zurückkauft, zahlt das Doppelte. Der Umweg kostet also immer Geld.

**Warum nicht zurück in die Emissionsreserve der Firma?** Dann bekäme die Firma
Aktien geschenkt, die sie zum vollen Kurs weiterverkaufen kann, während die Bank
die Hälfte bezahlt hat. Wer selbst Großaktionär ist, könnte daraus mit einem
Kreislauf Geld erzeugen.

**Alternative:** gar kein Notverkauf. Aktien zählen dann in der Not nicht, und
wer kein Geld hat, ist pleite. Hart, aber einfach.

---

## B – Bewertung

**Grundformel:**
```
Unternehmenswert = Substanzwert + Ertragswert
Aktienkurs       = Unternehmenswert / umlaufende Aktien
```

<a id="b-01"></a>
### B-01 – Substanzwert 🔴
Was die Firma **jetzt besitzt**. Wird live berechnet.
```
Substanzwert = Firmenkasse
             + Straßen zum Kaufpreis
             + Gebäude zum Baupreis
             + Projekte zum Buchwert (Baukosten, ggf. minus Schäden)
             + Beteiligungen (Aktien × Kurs der anderen Firma)
```
Bauen ist damit **wertneutral** (Geld wird zu Gebäude). Den Unterschied macht erst
der Ertragswert. Mieten erhöhen die Kasse und damit den Substanzwert **genau
einmal**.

**Alternative:** Gebäude nur zum Rückverkaufswert (50 %) ansetzen. Dann würde
jeder Bau den Kurs sofort senken. Das fühlt sich falsch an und bremst die
Entwicklung.

<a id="b-02"></a>
### B-02 – Ertragswert 🔴
Was die Firma **künftig voraussichtlich verdient**.

```
Ertragskraft (M pro Quartal) = Σ Straßen: aktuelle Miete × L
                             + Σ feste Projekterträge
                             − Σ Unterhalt

L = erwartete Landungen pro Feld und Quartal
  ≈ 0,12 × Anzahl aktiver Spieler   (Schätzwert, per Simulation prüfen)

Ertragswert = Ertragskraft × Multiplikator (Start: 2) × Konjunktur (0,8 … 1,2)
```

**Warum das keine Doppelzählung ist:** Erhaltene Miete liegt als Geld in der
Kasse; sie ist Vergangenheit und zählt im Substanzwert. Der Ertragswert bewertet
dagegen, was die Firma mit ihrem Bestand **künftig** wahrscheinlich verdient. Er
hängt nur vom Bestand ab (Mietstaffel, Projekte), **nicht** von tatsächlich
erhaltenen Zahlungen. Eine eingehende Miete von 1.500 M erhöht den Wert also um
genau 1.500 M und keinen Cent mehr.

**Zeitliche Regeln** (gegen Exploits X1/X3):
- Der Ertragswert wird **nur beim Quartalsabschluss** neu festgestellt.
  Verbesserungen zählen erst dann.
- **Verschlechterungen zählen sofort**: Wird eine Straße verkauft oder ein Projekt
  zerstört, fällt sein Anteil sofort weg (Vorsichtsprinzip).
- Eine neu gegründete Firma hat bis zum ersten Quartalsabschluss Ertragswert 0.

**Beispiel für die Erklärung in der App:**
```
TECH AG – Quartal 3 → Quartal 4
Unternehmenswert   10.000 M → 11.200 M
  + 800 M  Hotel Schlossallee (Ertragskraft +400 M/Q × 2)
  + 500 M  Mieteinnahmen (Kasse)
  − 100 M  Unterhalt Fabrik
Aktienkurs          100 M →   112 M
```

---

## D – Dividenden

<a id="d-01"></a>
### D-01 – Dividendenregel 🟡
**Vorschlag:**
- Höchstens **einmal pro Quartal**, der CEO entscheidet über Zeitpunkt und Höhe.
- **Maximal ausschüttbar** = `min(Bilanzgewinn, Kasse − Mindestreserve)`
  - **Bilanzgewinn** = alle Erträge (Mieten, Projekterträge, erhaltene
    Dividenden, Verkaufsgewinne) − alle Aufwendungen (Unterhalt, Ereignisse,
    Verkaufsverluste) − bisherige Dividenden. Startkapital und Zuschüsse zählen
    **nicht** dazu: Ausgeschüttet wird nur Verdientes.
  - **Mindestreserve** = `max(500 M, 10 % des Unternehmenswerts)`. Größere Firmen
    brauchen größere Polster, denn ihre Krisen sind auch größer.
- Verteilung pro umlaufender Aktie, abgerundet auf ganze M; der Rest bleibt in der
  Kasse.
- Dividenden an Firmen (bei Beteiligungen) gehen in deren Kasse und zählen dort
  als Ertrag.

**Beispiel:** 2.000 M bei 100 umlaufenden Aktien = 20 M je Aktie →
Patty (80) 1.600 M, Max (20) 400 M.

Die App zeigt dem CEO direkt: „Maximal ausschüttbar: 1.240 M (begrenzt durch
Reserve)“.

---

## K – Kontrolle & Konzern

<a id="k-01"></a>
### K-01 – CEO & Kontrolle 🔴 ✅❓
**Entschieden:** wie vorgeschlagen, mit deiner Ergänzung: *„außer das Unternehmen
wird verkauft oder es ist die einzige Möglichkeit, eine Pleite zu verhindern“*.

**Meine Lesart (bitte bestätigen):**
- Den **Verkauf des Unternehmens** darf der CEO nicht allein beschließen. Dafür
  braucht es > 50 % der Stimmen.
- **Ausnahme:** Ist der Verkauf die einzige Möglichkeit, eine Pleite abzuwenden,
  darf der CEO allein verkaufen (passt zu den Notverkäufen in R-04).

**Was heißt „Unternehmen verkaufen“ in unserem Modell?** Seine **eigenen Aktien**
darf jeder Aktionär jederzeit ohne Zustimmung verkaufen; das ist kein Verkauf
*durch* das Unternehmen. Gemeint sein kann also nur, dass die Firma ihr Vermögen
abgibt. Mein Vorschlag zur Abgrenzung:

| Entscheidung | Wer entscheidet |
|---|---|
| Häuser/Hotels bauen und verkaufen, Projekte bauen und abreißen, Reserve-Aktien anbieten, Aktien anderer Firmen handeln, Dividende (D-01) | CEO allein |
| **Straßen der Firma verkaufen**, Firma **auflösen**, Insidergeschäfte außerhalb des Preisbands (K-02) | > 50 % der Stimmen |
| Alles davon in **Zahlungsnot**, wenn es die Pleite abwendet | CEO allein |

**Weiterhin gilt:**
- **CEO = größter Aktionär.** Bei Gleichstand bleibt der amtierende CEO. Wer mehr
  Aktien kauft als der CEO, wird automatisch neuer CEO. **So einfach ist eine
  Übernahme.**
- Stimmen haben nur Aktien in Spieler- oder Firmenhand, nicht die
  Emissionsreserve und nicht der Bankbestand (A-06). Die Bank wird nie CEO.
- Ist eine Firma größter Aktionär, handelt deren CEO (später, mit K-04).
- **Abstimmung:** Die App stellt einen Antrag, die Aktionäre tippen Ja oder Nein.
  Hält der CEO selbst > 50 %, gilt der Antrag sofort als angenommen.
- Weitere Abstimmungsregeln (Sperrminorität, Pflichtangebot) halte ich für den
  Anfang für unnötig.

<a id="k-02"></a>
### K-02 – Insidergeschäfte 🟡
Gegen Exploit X2 (Selbstbedienung).
- **Insider** = der CEO und jeder Aktionär mit ≥ 25 %.
- Geschäfte zwischen Firma und Insider (Straßen, Aktien) sind nur zu **80 %–120 %
  des Referenzwerts** erlaubt. Referenzwert: Straße = Kaufpreis + Gebäude zum
  Baupreis; Aktie = Kurs.
- Außerhalb dieses Bands braucht es die Zustimmung der **übrigen** Aktionäre
  (Mehrheit ohne die Stimmen des Insiders).
- Hält der Insider 100 % der umlaufenden Aktien, entfällt die Regel, weil niemand
  geschädigt werden kann.
- Für alle anderen Firmengeschäfte gilt das allgemeine Band von 50 %–200 %.

<a id="k-03"></a>
### K-03 – Aktien bei Spielerbankrott 🔴 ⬜
*Durch G-05 (Ende durch Pleite) wichtiger geworden, daher jetzt 🔴.*
- **Bankrott gegenüber einem Spieler:** Wie alles andere gehen die Aktien an den
  Gläubiger.
- **Bankrott gegenüber der Bank:** Die Aktien gehen in den **Bankbestand** (A-06),
  den die Bank zum Kurs weiterverkauft.
  *(Geändert: Ursprünglich hatte ich die Emissionsreserve vorgeschlagen. Aus dem in
  A-06 beschriebenen Grund wäre das aber ein Geschenk an die Firma.)*
- **Alternative:** Versteigerung unter den übrigen Spielern. Spannender, aber eine
  zusätzliche Mechanik.

Besitzt kein aktiver Spieler mehr Aktien einer Firma, wird sie aufgelöst (R-04).

<a id="k-04"></a>
### K-04 – Beteiligungen zwischen Firmen 🟢
- Erlaubt. Der **Beteiligungsgraph muss azyklisch bleiben**: Der Server prüft vor
  jedem Aktienkauf durch eine Firma, ob ein Kreis entstehen würde (A → B → C → A),
  und lehnt ihn dann mit Erklärung ab.
- Ohne Kreise lässt sich jeder Wert eindeutig berechnen: zuerst die Firmen ohne
  Beteiligungen, dann die darüber.
- **Empfehlung:** erst in **Version 2**. Das Datenmodell sieht es von Anfang an
  vor (Aktionär kann Spieler **oder** Firma sein).

---

## P – Projekte

<a id="p-01"></a>
### P-01 – Projekt-Slots 🟡
**Vorschlag:** Nur Firmenstraßen haben Slots:
- Hotel → **1 Slot**
- Wolkenkratzer → **3 Slots**

Wird ein Gebäude zurückgebaut, müssen überzählige Projekte vorher abgerissen
werden, analog zur Regel „gleichmäßig bauen“.

**Alternative:** Slots nur mit Wolkenkratzer. Dann spielen Projekte erst sehr spät
im Spiel eine Rolle.

<a id="p-02"></a>
### P-02 – Projektkatalog 🟡
Zwei Familien, damit „klein vs. groß vs. gemischt“ eine echte Entscheidung wird:

- **Mietprojekte**: erhöhen die Miete beim Landen. Hohe Erträge, aber
  glücksabhängig und mit weniger Spielern weniger wert.
- **Ertragsprojekte**: zahlen beim Quartalsabschluss einen festen Ertrag. Stabil,
  unabhängig vom Würfelglück.

| Projekt | Slots | Baukosten | Wirkung | Risiko |
|---|---|---|---|---|
| 🏪 Laden | 1 | 500 M | Miete +300 M | niedrig |
| 🏢 Büros | 1 | 500 M | +120 M / Quartal | niedrig |
| 🛍️ Einkaufszentrum | 2 | 1.000 M | Miete +700 M | mittel |
| 🏭 Fabrik | 2 | 1.000 M | +280 M / Quartal | mittel |
| 🏨 Grand Resort | 3 | 1.500 M | Miete +1.150 M | hoch |
| 💻 Tech-Campus | 3 | 1.500 M | Ø +450 M / Quartal (Würfel: 0–900) | hoch |

**Designprinzip:** Große Projekte bringen pro Slot etwa 15–30 % mehr, haben aber
- ein Klumpenrisiko (eine Krise trifft alles),
- ein höheres Ereignisrisiko,
- keine Teilbarkeit (man kann nicht „ein Drittel“ verkaufen).

Kleine Projekte sind flexibel und streuen das Risiko.
*Alle Zahlen sind Platzhalter und werden per Simulation kalibriert.*

„Hotel“ heißt hier bewusst **Grand Resort**, damit es nicht mit dem Monopoly-Hotel
verwechselt wird. Zu deinem Beispiel: Fabrik (2) + 2 × Laden (1) wären 4 Slots;
auf einem Wolkenkratzer gingen nur Fabrik + 1 Laden.

<a id="p-03"></a>
### P-03 – Bauzeit, Abriss, Verkauf 🟡
- **Bauzeit:** Ein Projekt wird beim nächsten Quartalsabschluss fertig. Bis dahin
  wirkt es noch nicht. Das bringt Timing-Strategie ins Spiel und verhindert
  Endspiel-Pumpen.
- **Abriss:** jederzeit möglich, bringt 50 % des Buchwerts zurück.
- **Verkauf der Straße an einen Spieler:** Projekte müssen vorher abgerissen
  werden, denn Spieler können keine Projekte besitzen. Zwischen Firmen wandern
  Projekte mit der Straße.

**Dynamische Miete:**
```
Schlossallee (TECH AG)
Kartenmiete (Wolkenkratzer)  3.500 M
🏭 Fabrik                    —      (Ertragsprojekt, keine Miete)
🏪 Laden                     + 300 M
──────────────────────────────────
Aktuelle Miete               3.800 M
```
Als Basis gilt immer die **Kartenmiete** der Besitzrechtkarte, damit App und Karte
nie auseinanderlaufen.

<a id="p-04"></a>
### P-04 – Mietdeckel 🟢
Mega-Edition-Mieten sind schon hoch, Projekte kommen obendrauf. Eine einzige
Landung kann einen Spieler aus dem Spiel nehmen.
**Empfehlung:** zunächst **kein Deckel**, aber als Parameter vorbereitet
(z. B. „Projektaufschlag höchstens +100 % der Kartenmiete“). Nach den ersten
Testpartien entscheiden.

---

## R – Risiko & Ereignisse

<a id="r-01"></a>
### R-01 – Ereignisse auslösen 🟡
**Vorschlag:** Beim Quartalsabschluss würfelt **jeder CEO für seine Firma mit 2
Würfeln am Tisch** und trägt die Augensumme ein. Die Risikostufe (R-02) legt fest,
welche Augensummen ein Ereignis auslösen.

Warum physische Würfel? Niemand kann der App vorwerfen, „gezinkt“ zu sein, und es
fühlt sich an wie Brettspiel. **Alternative:** Die App würfelt sichtbar für alle.
Das ist schneller und als Einstellung wählbar.

<a id="r-02"></a>
### R-02 – Risikostufe 🟡
Jedes Projekt hat Risikopunkte (niedrig 1, mittel 2, hoch 3). Ihre Summe ergibt
die Stufe:

| Risikopunkte | Stufe | Krise bei Augensumme | Wahrscheinlichkeit | Glücksfall bei |
|---|---|---|---|---|
| 0–2 | niedrig | 2 | 2,8 % | 12 |
| 3–5 | mittel | 2–3 | 8,3 % | 12 |
| 6–8 | hoch | 2–4 | 16,7 % | 11–12 |
| 9+ | sehr hoch | 2–5 | 27,8 % | 11–12 |

Aggressives Wachstum bringt also mehr Chancen **und** mehr Gefahr, wie gewünscht.
Die App zeigt die Stufe dauerhaft an, damit niemand überrascht wird.

<a id="r-03"></a>
### R-03 – Ereigniskatalog 🟢
Klein starten, z. B.:
- 🔥 **Brand / Unfall:** Ein zufälliges Projekt ist beschädigt. Reparatur kostet
  50 % der Baukosten, sonst wird es stillgelegt.
- 🚪 **Mieterflucht:** Projektmieten ruhen ein Quartal.
- 📰 **Skandal:** Ertragswert −30 % bis zum nächsten Quartal.
- ⚖️ **Rechtsstreit:** 10 % der Kasse an die Bank.
- 🤝 **Großauftrag** (Glücksfall): ein zusätzlicher Quartalsertrag.
- 💡 **Durchbruch** (Glücksfall, nur Tech): Ertragswert +30 % bis zum nächsten
  Quartal.

Krisen skalieren mit der Firmengröße (Prozentwerte statt fester Beträge).

<a id="r-04"></a>
### R-04 – Zahlungsunfähigkeit & Insolvenz 🟡
Firmen können nie ins Minus gehen. Kann eine Firma eine Pflichtzahlung
(Ereignis, Unterhalt) nicht leisten:
1. Die Firma wird **gesperrt**: Bis zur Lösung sind keine anderen Aktionen möglich.
   So entstehen keine versteckten Schulden.
2. Der CEO wählt **Notverkäufe**: Projekte abreißen (50 %), Gebäude an die Bank
   (50 %, Monopoly-Regel), Straßen an die Bank (Hypothekenwert; die Straße wird
   wieder frei), Aktien anderer Firmen an die Bank (50 % des Kurses, A-06),
   Reserve-Aktien verkaufen, oder ein Aktionär leistet einen Zuschuss.
   In dieser Lage braucht der CEO keine Zustimmung (K-01).
3. Handelt der CEO nicht, führt die Bank die Notverkäufe in fester Reihenfolge aus.
4. Reicht alles nicht: **Insolvenz**. Alles wird verwertet, die Bank erhält, was da
   ist, die Aktien werden wertlos und die Firma wird aufgelöst. Straßen gehen an
   die Bank zurück.

Die Aktionäre verlieren nur ihre Aktien, nicht ihr Privatvermögen
(Haftungsbeschränkung).

<a id="r-05"></a>
### R-05 – Konjunktur 🟢
Eine globale Anzeige mit 5 Stufen: Rezession (×0,8), Abschwung (×0,9), Normal
(×1,0), Aufschwung (×1,1), Boom (×1,2). Sie wirkt als Faktor auf den Ertragswert
aller Firmen. Beim Quartalsabschluss kann sie sich um eine Stufe ändern
(Würfelwurf der Bank). So bewegen sich alle Kurse gemeinsam, wie eine
„Marktstimmung“, und das bleibt erklärbar.

---

## S – System, Rollen & Sicherheit

<a id="s-01"></a>
### S-01 – Beitritt 🔴
- Die Bank erstellt eine Partie. Die App zeigt einen **6-stelligen Code** (ohne
  verwechselbare Zeichen wie 0/O, 1/I) und einen **QR-Code**.
- Spieler geben Code + Nickname ein und warten in der **Lobby**. Die Bank sieht die
  Liste und kann Spieler entfernen. Nach Spielstart braucht ein Beitritt die
  Freigabe der Bank.
- Nicknames sind eindeutig (Groß-/Kleinschreibung egal), 2–16 Zeichen.
  „Bank“ und „System“ sind reserviert.
- Das Gerät erhält einen geheimen Schlüssel. Wer die Seite schließt und wieder
  öffnet, ist sofort wieder drin.

<a id="s-02"></a>
### S-02 – Bank als Mitspieler 🔴 ✅
**Entschieden:** Die Bank ist vorerst ein **Spielleiter**, der nicht mitspielt.
Das Vier-Augen-Prinzip entfällt damit zunächst. Das Datenmodell trennt Bank-Login
und Spieler trotzdem von Anfang an, damit „Banker spielt mit“ später ohne Umbau
nachrüstbar ist. Bank-Aktionen bleiben für alle im Verlauf sichtbar.

**Ursprüngliche Frage:** Ist der Banker ein Nicht-Spieler (Spielleiter), oder
spielt er mit?

**Damalige Empfehlung:** Die Bank ist eine **Rolle**, kein Wirtschaftsteilnehmer. Spielt der
Banker mit, hat er **zwei getrennte Identitäten** (Bank-Login + Spieler).
- Jede Bank-Aktion ist für **alle** im Verlauf sichtbar.
- Buchungen der Bank auf das **eigene** Spielerkonto (Korrektur, Auszahlung …)
  braucht die Bestätigung eines Mitspielers (**Vier-Augen-Prinzip**).

<a id="s-03"></a>
### S-03 – Gerätewechsel / Akku leer 🟡
Wer das Gerät wechselt, bekommt von der Bank einen **Wiederbeitritts-Code** und ist
damit auf dem neuen Gerät wieder derselbe Spieler. Das alte Gerät verliert den
Zugang.
**Alternative:** Beim Beitritt eine optionale 4-stellige PIN setzen.

<a id="s-04"></a>
### S-04 – Korrekturen 🟡
Nichts wird gelöscht oder überschrieben. Korrekturen sind **Gegenbuchungen** mit
Pflicht-Begründung, für alle sichtbar. Für häufige Fälle gibt es „Stornieren“
(z. B. einen versehentlichen Aktienkauf rückgängig machen), sofern seitdem nichts
darauf aufgebaut hat.

<a id="s-05"></a>
### S-05 – Accounts 🟢
- **Bank:** dauerhafter Login (Benutzername + Passwort), um mehrere Partien zu
  verwalten. Mehrere Geräte gleichzeitig möglich (z. B. iPad + Handy).
- **Spieler:** zunächst nur Gast-Identitäten pro Partie. **Später** optional ein
  Konto, mit dem man Gast-Identitäten verknüpfen kann (Statistiken, Historie).
  Das Datenmodell sieht dafür von Anfang an ein optionales Feld vor.

### Hinweis Markenrecht 🟢
„Monopoly“ ist eine Marke von Hasbro. Für private Partien ist das egal. Soll die
App irgendwann öffentlich erreichbar sein, sollten wir einen eigenen Namen nutzen
und keine Original-Kartentexte oder -grafiken einbetten.
