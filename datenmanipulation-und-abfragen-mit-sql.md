## Datenmanipulation und Abfragen mit SQL

Lösungen für die Aufgabe aus dem Tutorial Eintrag [Datenmanipulation und Abfragen mit SQL](https://informatik-ninja.de/tutorials/datenmanipulation-und-abfragen-mit-sqle#content-%C3%BCbungen)

## Übung 1
Angenommen, du hast eine Tabelle "produkte" mit den Spalten `id`, `produkt_name` und `preis`.
Die Geschäftsleitung hat beschlossen, die Preise für die "PlayStation 5" um 10% zu erhöhen.

Aufgabe: Schreibe eine SQL-Anweisung, die diese Preiserhöhung umsetzt.

### Lösung
```sql
UPDATE produkte
SET preis = preis * 1.10
WHERE produkt_name = 'PlayStation 5';
```

---

## Übung 2
Angenommen, du hast eine Tabelle "bestellungen" mit den Spalten `id`, `kunden_id`, `bestelldatum` und `status`.
Das Unternehmen möchte alte, stornierte Bestellungen aus der Datenbank entfernen, um Speicherplatz zu sparen.

Aufgabe: Schreibe eine SQL-Anweisung, die alle stornierten Bestellungen löscht. die älter als ein Jahr sind.

### Lösung
```sql
# Variante 1: Feste Datumsangabe
DELETE FROM bestellungen
WHERE status = 'storniert' and bestelldatum < "2023-01-01";

# Variante 2: Benutzen von CURRENT_DATE und INTERVAL Schlüsselwörtern
DELETE FROM bestellungen
WHERE status = 'storniert' and bestelldatum < CURRENT_DATE - INTERVAL '1 year';
```

`CURRENT_DATE` gibt das aktuelle Datum zurück und mit `- INTERVAL '1 year'` wird das aktuelle Datum um ein Jahr verringert.

Wichtige Anmerkungen:
- Vor der Ausführung solcher Anweisungen, besonders bei `DELETE`, ist es ratsam, ein Backup der Daten zu erstellen.
- Es kann nützlich sein, diese Anweisungen vorher als `SELECT`-Abfragen zu testen, um zu überprüfen, welche Datensätze betroffen sind.
- Bei großen Datenmengen sollte die Auswirkung auf die Datenbankleistung berücksichtigt werden und die Operation evtl. in kleinere Batches aufgeteilt werden.

---

## Übung 3

Schreibe eine SQL Abfrage, die alle Kunden mit ihren Bestellungen anzeigt, auch wenn sie keine Bestellungen haben. Sortieren Sie das Ergebnis nach dem Kundennamen.

### Lösung 
```sql
SELECT kunden.name, bestellungen.bestell_nr
FROM kunden
LEFT JOIN bestellungen ON kunden.id = bestellungen.kunden_id
ORDER BY kunden.name;
```

Wichtige Anmerkungen:
- Der `LEFT JOIN` stellt sicher, dass alle Kunden im Ergebnis erscheinen, auch wenn sie keine Bestellungen haben. In solchen Fällen wird die `bestell_nr` mit `NULL` belegt.
- Kunden mit mehreren Bestellungen werden mehrere Zeilen im Ergebnis haben, eine für jede Bestellung
- Die Sortierung nach Kundenname macht es einfach, alle Bestellungen eines Kunden gruppiert zu sehen

---

## Übung 4

Berechne den Gesamtumsatz pro Kunde und sortiere das Ergebnis nach dem höchsten Umsatz. 
Zeige nur Kunden mit einem Gesamtumsatz von mehr als 10.000 an.

### Lösung

```sql
SELECT kunden.name, SUM(bestellungen.betrag) AS gesamtumsatz
FROM kunden
INNER JOIN bestellungen ON kunden.id = bestellungen.kunden_id
GROUP BY kunden.id, kunden.name
HAVING SUM(bestellungen.betrag) > 10000
ORDER BY gesamtumsatz DESC;
```

Wichtige Anmerkungen:
- Der `INNER JOIN` stellt sicher, dass nur Kunden mit Bestellungen berücksichtigt werden
- `GROUP BY` ist notwending, um die Summe der Beträge pro Kunde zu berechnen
- `HAVING` ist notwending, um nur Kunden mit einer Summe von mehr als 10.000 zu berücksichtigen

---

## Übung 5
Finde alle Produkte, die teurer als der Durchschnittspreis sind. Zeige die Produktname, den Preis und um wie viel Prozent der Preis über dem Durchschnitt liegt.

### Lösung
```sql
SELECT 
    produkt_name, 
    preis, 
    ROUND((preis - (SELECT AVG(preis) FROM produkte)) / (SELECT AVG(preis) FROM produkte) * 100, 2) AS prozent_ueber_durchschnitt
FROM produkte
WHERE preis > (SELECT AVG(preis) FROM produkte)
ORDER BY prozent_ueber_durchschnitt DESC;
```

Wichtige Anmerkungen:
- Die Verwendung der Unterabfrage `(SELECT AVG(preis) FROM produkte)` ermittelt den durchschnittlichen Preis -> damit können wir den Durschnittspreis an verschiedenen Stellen der Hauptabfrage verwenden.
- Die `WHERE`-Bedingunge stellt sicher, dass nur Produkte über den Durchschnittspreis zurückgegeben werden.
- ` ROUND((preis - (SELECT AVG(preis) FROM produkte)) / (SELECT AVG(preis) FROM produkte) * 100, 2) AS prozent_ueber_durchschnitt` ist der komplexeste Teil der Abfrage. Hier wird der Prozentsatz, um den der Preis über dem Durschnitt liegt, berechnet:
  - `(SELECT AVG(preis) FROM produkte)` -> Durschnittspreis
  - `preis - (SELECT AVG(preis) FROM produkte)` -> absolute Differenz zum Durschnittspreis
  - `(preis - (SELECT AVG(preis) FROM produkte)) / (SELECT AVG(preis) FROM produkte) * 100` -> `(preis / durchschnitt) / durchschnitt * 100` -> Prozentsatz, um den der Preis über dem Durschnitt liegt

---

## Übung 6

Angenommen: Es gibt eine Tabelle `mitarbeiter` mit den Spalten `abteilung`, `name` und `gehalt`.

Aufgabe: Erstelle eine Abfrage, die für jede Abteilung den Mitarbeiter mit dem höchsten Gehalt anzeigt.

### Lösung

```sql
SELECT m1.abteilung, m1.name, m1.gehalt
FROM mitarbeiter AS m1
WHERE m1.gehalt = (
    SELECT MAX(m2.gehalt)
    FROM mitarbeiter AS m2
    WHERE m2.abteilung = m1.abteilung
);
```

Wichtige Anmerkungen:
- `SELECT MAX(m2.gehalt) FROM mitarbeiter AS m2 WHERE m2.abteilung = m1.abteilung` ist eine korrelierte Unterabfrage
  - `m2` ist ein Alias für die innere Abfrage der Mitarbeitertabelle
  - `MAX(m2.gehalt)` ermittelt das höchste Gehalt einer Abteilung
  - `WHERE m2.abteilung = m1.abteilung` stellt sicher, dass wir nur Gehälter innerhalb derselben Abteilung vergleichen
- Durch den Vergleich des Gehalts jedes Mitarbeiters mit dem Maximalgehalt seiner Abteilung werden nur die Mitarbeiter mit dem höchsten Gehalt ausgewählt.
- Diese Methode funktioniert auch, wenn es mehrere Mitarbeiter mit dem gleichen Höchstgehalt in einer Abteilung gibt - alle würden angezeigt werden.

---

## Übung 7

Angenommen, du hast eine Tabelle "bestellungen" mit den Spalten `id`, `produkt_id`, `bestelldatum`, und eine Tabelle "produkte" mit den Spalten `id`, `produkt_name` und `preis`.

Schreibe eine Abfrage, die alle Produkte auflistet, die in den letzten 30 Tagen nicht bestellt wurden.

### Lösung:

```sql
SELECT p.produkt_name
FROM produkte p
WHERE p.id NOT IN (
    SELECT DISTINCT produkt_id
    FROM bestellungen
    WHERE bestelldatum >= CURRENT_DATE - INTERVAL '30 days'
);
```

Wichtige Aspekte:
- Die Verwendung von `NOT IN` in Kombination mit einer Unterabfrage ermöglicht es uns, Produkte zu finden, die nicht in der Liste der kürzlich bestellten Produkte vorkommen.
- Die Unterabfrage fokussiert sich auf die letzten 30 Tage, was einen relevanten Zeitrahmen für die Analyse bietet.
  - `CURRENT_DATE` gibt das aktuelle Datum zurück.
  - `- INTERVAL '30 days'` subtrahiert 30 Tage vom aktuellen Datum.
- `DISTINCT` stellt sicher, dass jede Produkt-ID nur einmal gezählt wird, auch wenn sie mehrfach bestellt wurde -> verhindert, dass mehrfache Bestellungen desselben Produkts das Ergebnis beeinflussen.
