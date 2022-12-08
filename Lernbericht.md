# Lern-Bericht
Joel Jütte

✍️ ggf. Ihr Gruppenname und Ihre Gruppenmitglieder

## Einleitung
Im Modul 183 geht es um Applikationssicherheit.

✍️ Ein Satz, worum es in dem Projekt ging. Muss für einen externen Leser einfach zu verstehen sein.

## Was habe ich gelernt?
Von dem neu gelernten hat mich das Thema Interpreter Injections, welche es einem Angreifer ermöglichen Datenbanken oder andere Speicherdateien zu manipulieren, am meisten interessiert. 

✍️ Beschreiben Sie in einem Satz **eine** Sache, die Sie bei diesem Projekt gelernt haben und die Sie in diesem Lern-Bericht dokumentieren.

## Beschreibung
Bei Interpreter Injections probiert der Angreifer die Strucktur der Datenbank / Speicherdatei  zu erraten. Wenn er die Strucktur herausgefunden hat, kann er die Benutzereingabe so gestalten, dass neue oder andere Datensätze eingetragen werden. Es können auch Daten entfernt werden. Je nachdem wie viel der Angreifer weis, kann er sogar die gesamte Datenbank zerstören. 

Beispiel: Folgende Daten werden als Variabeln in das SQL Skript eingefügt.

```
username = Joel
password = 12345678
isAdmin = 0
```

So sieht es im Java Code aus

```Java
INSERT INTO user (useranme, password, isadmin) VALUES (
\"" + username + "\", \"" + password + "\" ,\"" + isAdmin + "\");
```

So wird es von SQL interpretiert

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
'Joel','12345678','0');
```

username und das password werden über ein Eingabefeld eingegeben. isAdmin ist im Benutzerobjekt gespeichert und wird so abgerufen. Sobald dies der Angreifer weiss, kann er folgendes in die Eingabefelder eingeben um einen Adminaccount zu erstellen. 

```
username: "Hacklord7000"
password: "meinPassword','1'); --"
```

Dies würde von SQL so interpretiert werden. 

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
'Hacklord7000','meinPassword','1'); --, 0);
```

Der Übrige SQL Code wird einfach asukommentiert. 

Wenn der Angreifer weiss, das die Tabelle user heisst, kann er die ganze Tabelle Löschen indem er folgendes in die Eingebefelder eingibt. 

```
Username: "Hacklord7000"
Password: "meinPassword','1'); DROP TABLE user;--"
```

Dies würde von SQL so interpretiert werden. 

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
'Hacklord7000','meinPassword','1');
DROP TABLE user; --, 0);
```

Wieder wird der restliche SQL Code einfach auskommentiert.

Um dem entgegenzuwirken gibt es Prepared statements. Diese sorgen dafür das SQL weiss, was anweisungen und was Daten sind. Die Variabeln werden durch Fragezeichen ersetzt, um danach später mit einer Prepared Statement Klasse befüllt zu werden. 

Das SQL Skript würde etwa so aussehen:

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
?, ?, ?);
```

Ein Beispiel aus einem Lernatelier Projekt, wo wir (Delia, Melanie und ich) mit Springboot die Prepared Statements verwendet haben. 
//Bild einfügen 

✍️ Verwenden Sie drei verschiedene Medien, um zu zeigen, was Sie gelernt haben. Zum Beispiel:

* Eine textliche Beschreibung
* Ein deutliches, aussagekräftiges Bild oder eine kommentierte Bildschirm-Aufnahme
* Ein gut dokumentierter Code-Fetzen
* Ein Link zu einem *selbst aufgenommenen* youtube-Video oder `.gif`.

## Verifikation

✍️ Erklären Sie kurz und bündig, inwiefern die von Ihnen verwendeten Medien zeigen, was Sie gelernt haben.

# Reflektion zum Arbeitsprozess

👍 Überlegen Sie sich jeweils etwas, was gut an Ihrer Arbeit lief; 

👎 und etwas, was nicht gut lief.

**VBV**: ✍️ Formulieren Sie davon ausgehend einen *handelbaren* Verbesserungsvorschlag.
