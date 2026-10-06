# 06 – Design-System „Black Edition“

> **Prototyp:** [Tischbörse Black Edition](https://claude.ai/artifact/QMDFSKLeRP8TGyWtcovcgB)
> (privat, bis du ihn teilst). Eine Kopie liegt in
> [`design/prototyp-black-edition.html`](../design/prototyp-black-edition.html) und
> lässt sich direkt im Browser öffnen.
> Auf dem iPad startet er in der Tischansicht, auf dem Handy in der Spieler-App.
> Direkt erreichbar über `#tisch` bzw. `#handy`.
>
> Die drei früheren Richtungen (A Spielbrett, B Karten, C Börsenparkett,
> [alter Entwurf](https://claude.ai/artifact/AAuTVJyJfbXu5EVuvEZaSk)) sind damit
> **ersetzt**.

---

## 1. Idee

**Schwarz, Silber, Licht.** Die App ist die digitale Fortsetzung des Spielplans der
Mega Black Edition: schwarz, mit Silberfolie, mit Farbstreifen.

| Prinzip | Bedeutung |
|---|---|
| **Das Brett ist ein Objekt im Raum** | Die Tischansicht zeigt den Spielplan als schwarze 3D-Platte mit Kante, Gebäuden und Hochhäusern, so wie er auf dem Tisch liegt |
| **Farbe ist Licht** | Farbgruppen erscheinen als leuchtende Streifen, Firmen als Lichtakzente (Hochhausspitze, Punkt, Rahmen). Flächen sind nie bunt |
| **Silber für Wert** | Kontostand, große Zahlen, Spielfiguren und Häuser sind silbern, wie die Figuren der Box |
| **Details auf Abruf** | Aus der Distanz ist alles ruhig. Namen und Mieten werden lesbar, sobald die Kamera auf ein Feld fliegt oder man etwas antippt |
| **Eine Hauptaktion pro Bildschirm** | Viel Schwarzraum, wenige Elemente, klare Hierarchie |

## 2. Farben

| Token | Wert | Verwendung |
|---|---|---|
| `void` | `#000000` | Grund (OLED-Schwarz) |
| `ink-1` … `ink-4` | `#0A0A0C` `#111114` `#1A1A1E` `#26262B` | Flächen, gestaffelt nach Höhe |
| `hair` / `hair-2` | Weiß 8 % / 15 % | Haarlinien, Rahmen |
| `silver-1` | `#F3F3F5` | Haupttext, große Zahlen |
| `silver-2` | `#B6B6BD` | Zweittext |
| `silver-3` | `#8A8A93` | Beschriftungen (Kontrast ≥ 5:1 auf Schwarz) |
| `up` / `down` | `#3DD68C` / `#FF6B5E` | Gewinn / Verlust, immer mit ▲/▼ |
| Glas | `rgba(16,16,19,.74)` + Unschärfe | HUD, Panels, Navigationsleiste |

**Farbgruppen** stammen direkt vom Foto des Spielplans:
Braun `#934725`, Hellblau `#B9E3F5`, Pink `#D9308C`, Orange `#F59003`, Rot `#E3000E`,
Gelb `#FEEC03`, Grün `#03943D`, Dunkelblau `#0267B5`.

**Firmen** bekommen eine Lichtfarbe, die sich von den Gruppen abhebt (im
Prototyp: TECH Cyan, BAU Violett, RETAIL Bernstein, HAFEN Mint). Bei der Gründung
wählt die App automatisch eine freie Farbe.

## 3. Typografie

Eine Familie, **Geist** (UI) und **Geist Mono** (Kürzel, Preise auf dem Brett,
Ticker). Die Hierarchie entsteht durch Größe, Strichstärke und Laufweite, nicht durch
viele Schriften:

| Rolle | Größe / Strich | Beispiel |
|---|---|---|
| Hero-Zahl | 46 px / 300, Silberverlauf | Kontostand auf der Metallkarte |
| Titel | 30–34 px / 300–400, Laufweite −2 % | „Quartal 4“, „Schlossallee“ |
| Text | 15–16 px / 400 | Listen, Erklärungen |
| Label | 11 px / 500, Versalien, Laufweite +18 % | „MIETE FÄLLIG“, „DEPOT“ |
| Daten | Geist Mono 11–12 px | `TECH`, `M 400` |

Alle Zahlen stehen in Tabellenziffern, damit nichts springt.

## 4. Signatur-Elemente

1. **Der 3D-Tisch** (Tischansicht, UI-03). Das echte 52-Felder-Brett als
   schwarze Platte:
   - Häuser und Hotels als Silberblöcke. Wolkenkratzer sind Glastürme mit einem
     Lichtstreifen in Firmenfarbe.
   - Ziehen dreht das Brett. Tippst du ein Feld an, fliegt die Kamera hin, und ein
     Glaspanel zeigt die Miete mit Aufschlüsselung.
   - Jede Mietzahlung am Tisch steigt als Lichtsäule aus dem Feld auf. Daneben
     erscheint „+3.800 M · Mia → TECH AG“.
   - Tippst du im Ticker eine Firma an, leuchten ihre Straßen auf, der Rest wird
     dunkel.
2. **Die Metallkarte** (Handy). Das Konto als schwarze, gebürstete Metallkarte,
   die sich mit dem Finger neigt. Der Kontostand rollt bei jeder Buchung
   (Zählwerk).
3. **Halten statt Tippen** (UI-02). Ab 1.000 M füllt sich der Knopf beim Halten von
   links mit Silber. Lässt man früh los, läuft er zurück.
4. **Das folgende Brett** (Ersatz für DS-03). Auf dem Handy wischt man durch eine
   Leiste aller Felder, und das 3D-Brett darüber fliegt jeweils mit. Ein Zwei-Finger-Zoom ist nie nötig.
5. **Silberne Spielfiguren** (UI-01). Eigene, schlichte Symbole (Hut, Auto, Schiff,
   Katze …) in silbernen Münzen. Es sind keine Nachbildungen der Original-Figuren.

## 5. Bewegung

| Moment | Dauer | Kurve |
|---|---|---|
| Eröffnung: Brett schwenkt in Position | 2,2 s | ease-in-out |
| Kamerafahrt zu einem Feld | 1,15 s | ease-in-out |
| Zählwerk (Kontostand, Kurs) | 1,1 s | ease-out |
| Sheet, Panel | 0,65 s | ease-out |
| Halten zum Bezahlen | 0,95 s | linear |
| Leerlauf: Brett „atmet“ (±4°) | 5 s Zyklus | Sinus |

Regeln: Jeder Effekt bedeutet etwas. Animiert werden nur `transform` und
`opacity`. Bei „Bewegung reduzieren“ entfallen Leerlauf, Kamerafahrten und
Lichtsäulen; die Werte springen direkt.

## 6. Technische Hinweise für die Umsetzung

- **3D ohne Bibliothek:** Das Brett besteht aus CSS-3D-Transformationen
  (`perspective`, `preserve-3d`). Das ist leicht, schnell, läuft überall und
  braucht kein WebGL.
- **Fallstricke** (im Prototyp gelöst):
  - `opacity`, `filter` und `overflow: hidden` auf einem 3D-Container machen ihn
    flach. Abgedunkelt wird deshalb nur der Inhalt eines Feldes.
  - Felder liegen 0,5 px über der Platte, damit nichts flimmert.
  - Beschriftungen über Feldern werden über `getBoundingClientRect` eines
    unsichtbaren Ankers im 3D-Raum positioniert und bleiben dadurch gestochen
    scharf.
- **Kamera:** `rotateX(neigen) rotateZ(drehen) scale(zoom) translate(…)`. Für ein
  Feld dreht die Kamera auf dessen Brettseite und zielt leicht Richtung Mitte,
  damit das Feld vorne steht.
- **Brettdaten** kommen aus
  [`data/board/mega-black-edition.json`](../data/board/mega-black-edition.json).

## 7. Entscheidungen

| ID | Frage | Stand |
|---|---|---|
| DS-01 | Richtung | ✅ Kombination aus Brett, Karten und Bewegung, aber in der neuen Sprache **Black Edition** |
| DS-02 | Hell oder dunkel? | ✅ **Schwarz** als Standard. Das weicht von meiner früheren Empfehlung „hell“ ab, folgt aber deinem Wunsch nach einem Black Design und dem Look der Box |
| DS-03 | Handy-Brett bei 52 Feldern | ❌ Zwei-Finger-Zoom abgelehnt → **„Das folgende Brett“** (§4.4), im Prototyp zum Ausprobieren |
| DS-04 | Töne | ✅ Optional, standardmäßig aus |
| DS-05 | Name der App | ⬜ Arbeitstitel **„Tischbörse“**. Ein eigener Name ist nötig, falls die App je öffentlich wird, denn „Monopoly“ ist eine Marke von Hasbro |
| DS-06 | Spielfiguren | ⬜ Eigene, schlichte Silber-Symbole (im Prototyp: Hut, Auto, Schiff, Katze). Offen: Welche Figuren liegen in deiner Box? Dann gestalte ich den passenden Satz |
