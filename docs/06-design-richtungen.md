# 06 – Design-Richtungen (Entwurf)

> Ergänzt das UI-Konzept ([`05-ui-konzept.md`](05-ui-konzept.md)) um Aussehen und
> Bewegung. Es gibt einen **klickbaren Prototyp** mit allen drei Richtungen:
> [Design-Richtungen auf claude.ai](https://claude.ai/artifact/AAuTVJyJfbXu5EVuvEZaSk)
> (privat, nur für den Besitzer sichtbar, solange er nicht geteilt wird).
>
> Der Prototyp nutzt das **klassische deutsche Brett (40 Felder)** und Beispielzahlen
> als Platzhalter. Die echte App verwendet die Daten der Mega Black Edition (G-01).

---

## Richtung A – Das Brett als Bühne

Der Bereich **Brett** zeigt das Spielbrett als Ring. Jedes Feld zeigt die
Farbgruppe, den Besitzer (Spieler-Kürzel oder Firmen-Badge) und die Gebäude.

| Effekt | Bedeutung |
|---|---|
| Feld antippen → es hebt sich an, Details öffnen sich | „Was ist hier los?“ in einem Tap |
| Firma antippen → ihre Straßen leuchten in Firmenfarbe, der Rest wird abgedunkelt | Konzerne auf einen Blick |
| Jede Mietzahlung pulsiert live auf dem Feld (Ring + „+3.800 M“) | Der ganze Tisch sieht, wo gerade Geld fließt |
| Im Inneren des Bretts: Quartal, Konjunktur, Firmen, Live-Feed | Die Wirtschaftslage in der Mitte des Spiels |

- **iPad:** Brett links, Detailbereich rechts. Ideal für die Bank und später die
  Tischansicht.
- **Handy:** kompaktes Brett mit Kürzeln statt Namen, Details im Bottom Sheet.
- **Stärke:** sofort vertraut; App und Brett verschmelzen.
- **Schwäche:** auf dem Handy klein. Mit den 52 Feldern der Mega-Edition werden
  die Felder noch schmaler (≈ 26 px), deshalb braucht das Handy eine
  Zoom-Geste oder eine Seitenansicht.

## Richtung B – Karten & Urkunden

Aktien erscheinen als **Aktienurkunden** mit Guilloche-Muster, Straßen als
**Besitzrechtkarten**. Man wischt durch die Karten; Antippen dreht eine Karte in 3D
um.

- **Rückseite einer Urkunde:** wem die Firma gehört (Balken), letzte Dividende,
  „5 Aktien kaufen“ aus der Reserve. Nach dem Kauf erscheint ein Stempel
  „+5 gekauft“.
- **Rückseite einer Besitzrechtkarte:** Grundbuch-Info und „Firma gründen“, sobald
  die Farbgruppe vollständig ist.
- **Stärke:** haptisch, mit Sammelgefühl; Besitz wird greifbar.
- **Schwäche:** Bei vielen Positionen fehlt der Überblick, deshalb steht eine
  kompakte Liste darunter.

## Richtung C – Börsenparkett

Ein dunkles, klares Börsen-Layout:

| Effekt | Bedeutung |
|---|---|
| Laufband mit allen Kursen | Börsengefühl, ohne dass man hinschauen muss |
| **Rollende Ziffern** bei jeder Änderung | Man *sieht*, dass sich ein Wert ändert, statt dass er springt |
| Mini-Kurslinien, die jedes Quartal weiterwachsen | Entwicklung auf einen Blick |
| Zeilen blitzen beim Quartalsabschluss grün oder rot auf, immer mit Pfeil | Gewinner und Verlierer sofort erkennbar |
| Quartalsbericht fliegt als Karte ein | Der Moment „Quartalszahlen“ wird zum Ereignis |
| **Münzen fliegen ins Konto** bei einer Dividende | Belohnungsmoment |

- **Stärke:** Spannung und Klarheit.
- **Schwäche:** Ohne Brettbezug wirkt es wie eine Finanz-App.

---

## Empfehlung: Kombination statt Entweder-oder

| Baustein | Herkunft | Wo |
|---|---|---|
| Bewegungssprache: rollende Ziffern, Aufblitzen, Münzen, Quartalsbericht | C | überall |
| Aktien und Straßen als Karten (umdrehbar) | B | Start/Depot, Firmenansicht |
| Brett mit Live-Puls und Firmen-Hervorhebung | A | Bereich „Brett“, Bank-iPad, später Tischansicht |
| Helles Grundthema; der Dunkelmodus nutzt den Parkett-Look | A/B hell, C dunkel | Systemeinstellung |

So bleibt das Brett im Mittelpunkt, Besitz fühlt sich greifbar an, und Geld- und
Kursbewegungen sind spürbar, ohne dass die App überladen wirkt.

## Bewegungsregeln

1. **Jeder Effekt bedeutet etwas.** Geld bewegt sich → Ziffern rollen. Besitz
   wechselt → Stempel. Kurs ändert sich → Aufblitzen mit Pfeil. Kein Effekt nur
   zur Deko.
2. **Kurz:** 150–900 ms. Nichts blockiert die Bedienung, und niemand wartet auf
   eine Animation.
3. **Flüssig auch auf älteren Handys:** Animiert werden nur `transform` und
   `opacity`.
4. **Barrierefrei:** Bei „Bewegung reduzieren“ (`prefers-reduced-motion`) sind alle
   Animationen aus, und Werte springen direkt.
5. **Nicht nur Farbe:** Steigen und Fallen immer zusätzlich mit ▲/▼ und Vorzeichen.
6. **Ruhig bleiben:** Live-Pulse für Mieten, aber nichts blinkt dauerhaft. Töne
   sind optional und standardmäßig aus.

## Offene Design-Fragen

| ID | Frage | Empfehlung |
|---|---|---|
| DS-01 | Welche Richtung? | **Kombination** wie oben |
| DS-02 | Hell oder dunkel als Standard? | **Hell**; der Dunkelmodus folgt der Systemeinstellung |
| DS-03 | Brett auf dem Handy bei 52 Feldern | **Zoombares Brett** (zwei Finger) + Bottom Sheet; alternativ eine Ansicht pro Brettseite |
| DS-04 | Töne (Münzklimpern bei Dividende, Kassenklingeln bei Miete)? | **Optional, standardmäßig aus** |
