# Arbeitsvereinbarungen

## Projekt
WebApp-Erweiterung für das physische Monopoly-Brettspiel (Mega-Edition): Unternehmen,
Aktien, Dividenden, Bewertung, Projekte, Ereignisse. Die App erweitert das Brett,
sie ersetzt es nicht. Andere Editionen, Falschgeld, Black Market u. Ä. gehören
nicht zum Projekt.

## Quellen der Wahrheit
- `docs/00-vision.md`: beschlossene Regeln. Nur nach Rücksprache ändern.
- `docs/02-entscheidungen.md`: offene und getroffene Entscheidungen (IDs wie `A-02`).
  Wird eine Entscheidung getroffen, Status und Text dort aktualisieren.
- `docs/03-architektur.md`: technische Architektur.
- `docs/04-regelwerk.md`: konsolidiertes Regelwerk (✅ entschieden / 💡 Vorschlag).
  Die Engine setzt nur ✅-Regeln um. Mit `02-entscheidungen.md` synchron halten.

## Zusammenarbeit
- Dokumentation und Kommunikation auf Deutsch; Code-Bezeichner auf Englisch.
- Keine Spielregeln eigenmächtig erfinden oder ändern. Vorschläge machen, Rückfragen
  stellen, Widersprüche und Exploits offen ansprechen.
- In Etappen arbeiten (siehe Architektur §15). Kein Feature-Code vor Freigabe der
  zugehörigen Regeln.

## Technische Leitlinien
- Die Spiellogik liegt ausschließlich in `packages/engine`: rein und deterministisch,
  ohne I/O. Der Server ist autoritativ und vertraut dem Client nie.
- Geld ist immer eine ganze Zahl in M. Kein Konto (außer der Bank) wird negativ.
- Die Aktienzahl einer Firma ist nach der Gründung unveränderlich.
- Das Ereignisprotokoll wird nur ergänzt. Korrekturen sind Gegenbuchungen.
- Jede berechnete Zahl (Miete, Wert, Kurs) braucht eine Aufschlüsselung.
