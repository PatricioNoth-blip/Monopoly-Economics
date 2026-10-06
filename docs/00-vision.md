# 00 – Vision & beschlossene Grundlagen

> Dieses Dokument hält fest, was **bereits entschieden** ist. Es ist die Referenz,
> gegen die alle Vorschläge geprüft werden. Änderungen hier nur nach ausdrücklicher
> Absprache.

## Kernidee

**Klassisches Monopoly + Aktien + Unternehmen + Projekte + digitale Wirtschaft.**

- Das physische Brettspiel (Mega-Edition mit Wolkenkratzern) bleibt das Zentrum.
- Die WebApp **erweitert** das Brettspiel, sie **ersetzt** es nicht.
- Die App übernimmt, was mit Papier und Taschenrechner zu kompliziert wäre:
  Unternehmen, Aktien, Dividenden, Bewertung, Projekte, Ereignisse, Protokoll.
- Komplexität darf im Hintergrund existieren. Der Spieler muss aber jederzeit
  verstehen: **Was ist passiert, und warum?**

## Nicht Teil des Projekts

Andere Editionen, Falschgeld, Black Market und ähnliche Erweiterungen.

## Beschlossene Regeln

### Rollen
- **Bank**: eigener Login, zentrale Instanz der Partie, Verwaltungsrechte
  (Partie erstellen/starten/pausieren/beenden, Spieler verwalten, Geld ein- und
  auszahlen, Ereignisse auslösen/bestätigen, Fehler korrigieren, Spieler sperren).
  Die Bank darf **keinen unfairen wirtschaftlichen Vorteil** haben.
- **Spieler**: Beitritt wie bei Kahoot – Game-Code + Nickname, kein Pflicht-Account.
  Der Nickname ist innerhalb der Partie eindeutig.

### Geld
- Jeder Spieler hat ein digitales Konto. Kontostände ändern sich **nur durch
  protokollierte Transaktionen**, nie durch direktes Setzen.
- Ein- und Auszahlungen zwischen digitalem und physischem Geld führt die Bank durch
  und sie werden protokolliert.
- Unternehmensgeld und Privatgeld sind **strikt getrennt**.

### Aktien
- Jedes Unternehmen hat eine **feste Anzahl Aktien**. Es werden **niemals** neue
  Aktien erzeugt.
- Beim Handel wechseln Aktien nur den Besitzer; das Unternehmen bleibt unverändert.
- Aktien bedeuten Vermögensanteil **und** Kontrolle (Mehrheit über 50 %).
- Übernahmen laufen ausschließlich über den Kauf bestehender Aktien.

### Unternehmen
- Gründung setzt grundsätzlich eine vollständige Farbgruppe voraus
  (Details offen).
- Die Gründung kostet Geld: Die **Gründungskosten** gehen an die Bank, das
  **Startkapital** gehört danach dem Unternehmen.
- Die Gründung soll nicht zu billig sein. Lieber angemessene Kosten und genug
  Startkapital als viele künstliche Startnachteile.
- Ein Unternehmen kann besitzen: Immobilien, Häuser, Hotels/Wolkenkratzer,
  Projekte, Geld, Aktien anderer Unternehmen.
- Weder Aktionäre noch CEO können Unternehmensvermögen privat entnehmen.
- **Keine Kredite, keine Schulden, kein Minus, keine Anleihen.** Wer nicht zahlen
  kann, verkauft Vermögen oder geht in die Insolvenz.

### Immobilien & Miete
- Private Immobilie: Die Miete geht an den Spieler.
  Unternehmensimmobilie: Die Miete geht an das Unternehmen.
- Wer auf einer Unternehmensimmobilie landet, zahlt **persönlich**. Das Unternehmen
  übernimmt keine privaten Mieten.
- Normale Immobilien folgen den normalen Monopoly-Regeln.
- Stark entwickelte Unternehmensimmobilien können eine **dynamische Miete** haben.
  Die App muss jede Miete aufschlüsseln können.

### Projekte
- Entwickelte Unternehmensgrundstücke (Basis: Wolkenkratzer) haben Projekt-Slots.
- Projekte belegen 1, 2 oder 3 Slots (z. B. Laden, Fabrik, Technologie, Industrie).
- Die strategische Entscheidung lautet: viele kleine Projekte, ein großes oder eine
  Mischung.

### Bewertung & Kurs
- Der Unternehmenswert wird automatisch berechnet.
- **Kein doppeltes Bewerten desselben Geldes.**
- Der Wert ist mehr als Immobilien + Cash: Er enthält auch eine Komponente für die
  **Ertragskraft**.
- Der Aktienkurs folgt dem Unternehmenswert und ist nachvollziehbar aufgeschlüsselt.

### Dividenden
- Werden anteilig nach Aktienbesitz ausgeschüttet; die Aktienanzahl bleibt gleich.
- Eine Reserve-/Ausschüttungsregel verhindert, dass ein Unternehmen sich
  handlungsunfähig ausschüttet.

### Beteiligungen
- Unternehmen dürfen Aktien anderer Unternehmen kaufen.
- Zirkuläre Beteiligungen (A → B → C → A) werden verboten oder sauber behandelt.

### Risiko
- Unternehmen haben höhere Chancen **und** Risiken als private Investments.
- Statt dauerhaft hoher Kosten gibt es **seltene, größere Ereignisse**.

### Strategien
Mindestens drei Strategien müssen tragfähig sein und sich kombinieren lassen:
**Privatinvestor**, **Aktieninvestor**, **Unternehmer**.

## Technische Grundanforderungen

- Echte WebApp im Browser, ohne Installation.
- Mobile First: Smartphone, iPad (eigenes Layout, keine vergrößerte Handyseite),
  Desktop. Vollständig per Touch bedienbar.
- **Echtzeit**: Alle verbundenen Geräte sehen praktisch sofort denselben Stand,
  ohne Neuladen.
- Der Spielstand wird zentral gespeichert und übersteht das Schließen des Browsers.
- Alle kritischen Änderungen werden **serverseitig validiert**. Der Server vertraut
  dem Browser nicht.
- Eine lückenlose, nachvollziehbare Transaktionshistorie.

## Arbeitsweise

Wir arbeiten strukturiert: Anforderungen → offene Regeln → Game-Design →
Datenmodell → Architektur → UI-Konzept → Backend → Echtzeit → Frontend → Tests →
weitere Features.
Regeln werden gemeinsam entwickelt, nicht eigenmächtig erfunden.
