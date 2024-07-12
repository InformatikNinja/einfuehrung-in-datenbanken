## Grundlegende SQL-Befehle für Einsteiger

Lösungen für die Aufgabe aus dem Tutorial Eintrag [Grundlegende SQL-Befehle für Einsteiger](https://informatik-ninja.de/tutorials/grundlegende-sql-befehle#content-%C3%BCbungen)

## Übung 1
Erstelle eine neue Tabelle `Benutzer` in der `Bibliothek`-Datenbank mit den Feldern `user_id` (Primärschlüssel), `name`, `adresse`, `geburtstag`, `eMail`(eindeutig) und `telefonnummer`.

### Lösung
~~~sql
CREATE TABLE Benutzer (
    user_id INT PRIMARY KEY AUTO INCREMENT,
    name VARCHAR(100) NOT NULL,
    adresse VARCHAR(255),
    geburtstag DATE,
    eMail VARCHAR(100) UNIQUE,
    telefonnummer VARCHAR(15)
);
~~~

## Übung 2
Füge mindestens 10 Benutzer in die `Benutzer` Tabelle ein, mit verschiedenen Namen, Adressen und Geburtstagen.

### Lösung
~~~sql
INSERT INTO Benutzer (name, adresse, geburtstag, eMail, telefonnummer)
VALUES ('Max Mustermann', 'Musterstraße 1', '1970-01-01', 'max@example.com', '1234567890'),
       ('Erika Musterfrau', 'Beispielweg 2', '2000-01-01', 'erika@example.com', '0987654321'),
       ('John Doe', 'Test 1', '2020-12-31', 'john.doe@example.com', '1122334455'),
       ('Jane Doe', 'Test 1', '2021-12-31', 'jane.doe@example.com', '1122334455'),
       ('Luke Skywalker', 'Tatooine 42', '1977-05-04', 'luke.skywalker@example.com', '123459876'),
       ('Leia Organa', 'Alderan 1', '1977-05-04', 'leia.organa@example.com', '987612345'),
       ('Alice', 'Sicherheitsweg 1', '1980-01-01', 'alice@example.com', '9988776655'),
       ('Bob',  'Sicherheitsweg 42', '1980-01-01', 'bob@example.com', '991188227733'),
       ('Tick Duck', 'Entenhausen', '1937-10-17', 'tick@example.com', '0123456789'),
       ('Trick Duck', 'Entenhausen', '1937-10-17', 'trick@example.com', '0123456789'),
       ('Track Duck', 'Entenhausen', '1937-10-17', 'track@example.com', '0123456789')
;
~~~

## Übung 3
Schreibe eine `SELECT`-Abfrage, die alle Benutzer zurückgibt die mindestens 18 Jahre alt sind.

### Lösung
~~~sql
SELECT * FROM Benutzer WHERE geburtstag >= '2006-01-01';

-- alternative
SELECT * FROM Benutzer WHERE YEAR(geburtstag) >= 2006;
~~~

Beispiel-Rückgabe:
~~~txt
|John Doe|Test 1|2020-12-31|john.doe@example.com|1122334455
|Jane Doe|Test 1|2021-12-31|jane.doe@example.com|1122334455
~~~

## Übung 4
Schreibe eine `SELECT`-Abfrage, die alle Benutzer zurückgibt die eine E-Mail-Adresse von Googlemail haben (`...@googlemail.com` oder `...@gmail.com`)

### Lösung
~~~sql
SELECT * FROM Benutzer WHERE eMail LIKE '%@googlemail.com' OR eMail LIKE '%@gmail.com';
~~~

## Übung 5
Schreibe eine `SELECT`-Abfrage, die den Namen und das Geburtsdatum der 3 ältesten Benutzer zurückgibt.

### Lösung
~~~sql
SELECT name, geburtstag FROM Benutzer 
ORDER BY geburtstag ASC
LIMIT 3;
~~~

Bsp-Rückgabe:
~~~txt
Tick Duck|1937-10-17
Trick Duck|1937-10-17
Track Duck|1937-10-17
~~~
