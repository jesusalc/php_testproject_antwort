Testprojekt
===========

Beschreibung 
------------
Es soll eine Webanwendung zum Erfassen von Postsendungen erstellt werden.

Der User erfasst Sendungen über ein Webformular. Diese werden in einer DB gespeichert.

Es wird zusätzlich eine flexibel einsetzbare Helper-Klasse benötigt, die bestimmte Informationen zum Sendungsbestand berechnet (s.u.). Die Helper-Klasse greift selbst nicht direkt auf die DB zu, sondern erhält die Sendungen, die berücksichtigt werden sollen im Code in der Form $helper->addSending(...)

Das Projekt besteht aus folgenden Aufgabenbereichen:
----------------------------------------------------
* Anlegen einer geeigneten DB-Struktur. SQL-File zum Anlegen der DB bitte im Ordner 'data' ablegen. Als DB bitte Postgres verwenden.
* Erstellen eines Webformulars und des benötigten JS-Codes. Hier ist die Verwendung von Bibliotheken (z.B. jQuery, ExtJs, jQueryUI etc.) erlaubt.
* Erstellen einer addSending.php mit einer Funktion zum Speichern der Formular-Eingaben in der DB
* Erstellen von Klassen für die Sendungsarten. Die Klassen haben u.a. eine Methode save(), um das Objekt in der DB anzulegen. (Funktionen zum laden aus der DB müssen nicht umgesetzt werden)
* Erstellen der Helper-Klasse CourierHelper, der man Sendungen übergeben kann und die zu den übergebenen Sendungen verschiedene Informationen zurückliefert (Details s.u.).


Anforderung an die Weboberfläche
------------------------------------
Formular zur Erfassung von Sendungen

* Auswahl:
  - Paket national
  - Paket international
  - Brief national
  - Brief international

* übrige Felder nur anzeigen, wenn sie notwendig sind (s. Beschreibung der einzelnen Sendungsarten)
* über das Webformular sollen folgende Daten erfasst werden: Sendungsart, Empfängername, Eingangsdatum, Größe und Gewicht der Sendung
* Eingangsdatum als Datepicker
* Speichern per Ajax
* per JS prüfen, dass alle Felder gefüllt sind. Es wird nur gespeichert, wenn keine Daten fehlen
* nach Speichern Ausgabe "Sendung an {Empfänger} wurde erfasst. Vorausichtliche Zustellung am ..., Preis: ..."

Beschreibung der einzelnen Sendungsarten
--------------------------------------------
**Sendungen allgemein**
* Empfängername
* eindeutige Tracking-Id
* Eingangsdatum
* Zustelldauer 
  - Regeln hierzu:
    - Briefe National 1 Tag, Interational 2 Tage
    - Pakete National 2 Tage, International 7 Tage
            

**Interationale Sendungen (Pakete und Briefe)**
* Zollkosten
* Land (Frankreich, Luxembourg, Belgien)

**Briefe**
* Gewicht in g

**Pakete**
* Höhe, Breite, Länge in cm
* Gewicht in g
* Funktion zum berechnen des Preises

**Preise**
* Paket national
  - Volumen < 6000 cm2, Gewicht <= 2 kg => 3,95 €
  - Volumen < 6000 cm2, Gewicht > 2 kg =>  6,95 €
  - Volumen >= 6000 => 7,95 €

* Paket international
  - Volumen < 4000 cm2 -> 6,95
  - Volumen < 6000 cm2, Gewicht <= 2 kg => 8,95 €
  - Volumen < 6000 cm2, Gewicht > 2 kg => 10,95 €

* Brief national
  - Gewicht <= 100g 0,70 €
  - Gewicht > 100g => 1,60 €

* Brief international
  - Gewicht <= 100g => 0,90 €
  - Gewicht > 100g => 2,10 €
  - Gewicht >= 300g => 4,40 €

**Funktionen von CourierHelper**
* Funktion, um eine Sendung zu registrieren (->addSending())
* Funktion zum Berechnen des Gesamtpreises aller Sendungen
* Berechnung, wie viele internationale Sendungen, wie viele nationale Sendungen und wieviele Sendungen insgesamt vorliegen
* Berechnung des Gesamtgewichts der Pakete und des Gesamtgewichts der Briefe
* Funktion, die ein Datum entgegennimmt und ausgibt, wieviele Pakete an diesem Tag ausgeliefert werden (s. Zustelldauer weiter oben)

Vorgaben
--------
* Repository forken und nach Fertigstellung einen Pull-Request stellen.
* Mit mehreren kleineren Commits arbeiten, damit wir das Vorgehen nachvollziehen können.
* Daten werden in Postgres-DB gespeichert.
* Für PHP keine externeren Bibliotheken bzw. Composer packages verwenden
* Bei JS ist die Verwendung von Bibliotheken erlaubt
* Ergebnis in git Repository ablegen
* SQL File für DB in Ordner data ablegen
