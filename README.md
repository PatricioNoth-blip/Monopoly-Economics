# Monopoly Economics

Eine WebApp, die das klassische Monopoly-Brettspiel (Mega-Edition) um eine digitale
Wirtschaftsebene erweitert:

🏠 Immobilien → 🏢 Unternehmen → 📈 Aktien → 💰 Dividenden → 📊 Unternehmenswert →
🏗️ Projekte → 📉 Risiken & Ereignisse

Das Brett bleibt physisch. Die App übernimmt, was mit Papier und Taschenrechner zu
kompliziert wäre, und zeigt allen Geräten am Tisch in Echtzeit denselben Stand.

## Status

**Phase 1 – Regelwerk & UI-Konzept.** Es gibt noch keinen Anwendungscode. Die
Kernregeln und die Architektur sind entschieden; als Nächstes folgt der
Rechenkern (Engine).

| Dokument | Inhalt |
|---|---|
| [`docs/00-vision.md`](docs/00-vision.md) | Vision und bereits beschlossene Regeln |
| [`docs/01-analyse.md`](docs/01-analyse.md) | Konzeptanalyse: Widersprüche, Exploits, Balancing |
| [`docs/02-entscheidungen.md`](docs/02-entscheidungen.md) | Offene Designentscheidungen mit Empfehlungen |
| [`docs/03-architektur.md`](docs/03-architektur.md) | Technische Architektur, Datenmodell, Etappenplan |
| [`docs/04-regelwerk.md`](docs/04-regelwerk.md) | Regelwerk v0.1: entschiedene Regeln + offene Vorschläge |
| [`docs/05-ui-konzept.md`](docs/05-ui-konzept.md) | UI-Konzept: Navigation, Abläufe, Wireframes für Smartphone und iPad |

## Geplanter Technik-Stack (Vorschlag)

- **TypeScript** in Server, Browser und Spiellogik
- **Engine**: reiner, getesteter Rechenkern für alle Regeln
- **Server**: Node.js + WebSocket (Socket.IO), autoritativ
- **Datenbank**: PostgreSQL mit unveränderlichem Ereignisprotokoll
- **Frontend**: React-PWA, Mobile First (Smartphone, iPad, Desktop)

Details und Begründung: [`docs/03-architektur.md`](docs/03-architektur.md).

## Geplante Struktur

```
apps/server      Server: HTTP + WebSocket, Spielräume, Speicherung
apps/web         WebApp für Spieler und Bank
packages/engine  Spielregeln, Bewertung, Mieten (reine Logik)
packages/protocol Gemeinsame Schemas für Befehle und Ereignisse
tools/sim        Balancing-Simulation
data/board       Brettdaten
docs/            Konzept & Entscheidungen
```

## Hinweis

Privates Hobbyprojekt. „Monopoly“ ist eine eingetragene Marke von Hasbro. Dieses
Projekt steht in keiner Verbindung zu Hasbro.
