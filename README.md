# Einführung in Datenbanken mit MySQL

Übungen und Lösungen für die Tutorial Reihe [Einführung in Datenbanken mit MySQL](https://informatik-ninja.de/tutorials/einfuehrung-datenbanken-mysql)

## Grundlegende SQL-Befehle für Einsteiger

Diese Übungen decken die wichtigsten Konzepte ab, die wir im  Tutorial [Grundlegende SQL-Befehle für Einsteiger](https://informatik-ninja.de/tutorials/grundlegende-sql-befehle#content-%C3%BCbungen) behandelt haben. Versuche sie selbstständig zu lösen, bevor du dir die Lösungen anschaust. Die praktische Anwendung ist der beste Weg, um SQL zu lernen und zu beherrschen.

- **Übung 1**: Erstelle eine neue Tabelle `Benutzer` in der `Bibliothek`-Datenbank mit den Feldern `user_id` (Primärschlüssel), `name`, `adresse`, `geburtstag`, `eMail` und `telefonnummer`.
- **Übung 2**: Füge mindestens 10 Benutzer in die `Benutzer` Tabelle ein, mit verschiedenen Namen, Adressen und Geburtstagen.
- **Übung 3**: Schreibe eine `SELECT`-Abfrage, die alle Benutzer zurückgibt die mindestens 18 Jahre alt sind.
- **Übung 4**: Schreibe eine `SELECT`-Abfrage, die alle Benutzer zurückgibt die eine E-Mail-Adresse von Googlemail haben (`...@googlemail.com` oder `...@gmail.com`)
- **Übung 5**: Schreibe eine `SELECT`-Abfrage, die die 10 ältestens Benutzer zurückgibt.

Zu den [Lösungen](grundlegende-sql-befehle.md)

## Datenmanipulation und Abfragen mit SQL
Diese Übungen decken die wichtigsten Konzepte ab, die wir im  Tutorial [Datenmanipulation und Abfragen mit SQL](https://informatik-ninja.de/tutorials/datenmanipulation-und-abfragen-mit-sql#content-%C3%BCbungen) behandelt haben. Versuche sie selbstständig zu lösen, bevor du dir die Lösungen anschaust. 
Die praktische Anwendung ist der beste Weg, um SQL zu lernen und zu beherrschen.

- **Übung 1**: 
  - Angenommen, du hast eine Tabelle "produkte" mit den Spalten `id`, `produkt_name` und `preis`.
    Die Geschäftsleitung hat beschlossen, die Preise für die "PlayStation 5" um 10% zu erhöhen.
  - **Aufgabe:**  Schreibe eine SQL-Anweisung, die diese Preiserhöhung umsetzt
- **Übung 2**: 
  - Angenommen, du hast eine Tabelle "bestellungen" mit den Spalten `id`, `kunden_id`, `bestelldatum` und `status`.
    Das Unternehmen möchte alte, stornierte Bestellungen aus der Datenbank entfernen, um Speicherplatz zu sparen.
  - **Aufgabe:** Schreibe eine SQL-Anweisung, die alle stornierten Bestellungen löscht. die älter als ein Jahr sind.
- **Übung 3**: Schreibe eine SQL Abfrage, die alle Kunden mit ihren Bestellungen anzeigt, auch wenn sie keine Bestellungen haben. Sortieren Sie das Ergebnis nach dem Kundennamen.
- **Übung 4**: Berechne den Gesamtumsatz pro Kunde und sortiere das Ergebnis nach dem höchsten Umsatz.
  Zeige nur Kunden mit einem Gesamtumsatz von mehr als 10.000 an.
- **Übung 5**: Finde alle Produkte, die teurer als der Durchschnittspreis sind. Zeige die Produktname, den Preis und um wie viel Prozent der Preis über dem Durchschnitt liegt.
- **Übung 6**:
  - Angenommen es gibt eine Tabelle `mitarbeiter` mit den Spalten `abteilung`, `name` und `gehalt`.
  - **Aufgabe**: Erstelle eine Abfrage, die für jede Abteilung den Mitarbeiter mit dem höchsten Gehalt anzeigt.
- **Übung 7**:
  - Angenommen, du hast eine Tabelle "bestellungen" mit den Spalten `id`, `produkt_id`, `bestelldatum`, und eine Tabelle "produkte" mit den Spalten `id`, `produkt_name` und `preis`.
  - Schreibe eine Abfrage, die alle Produkte auflistet, die in den letzten 30 Tagen nicht bestellt wurden.

Zu den [Lösungen](datenmanipulation-und-abfragen-mit-sql.md)
