# Lern-Bericht
Joel Jütte

## Einleitung
Im Modul 183 geht es um Applikationssicherheit.

## Was habe ich gelernt?
Von dem neu Gelernten hat mich das Thema "Interpreter Injections", welche es einem Angreifer ermöglichen, Datenbanken oder andere Speicherdateien zu manipulieren, am meisten interessiert. 

## Beschreibung
Bei "Interpreter Injections" probiert der Angreifer die Strucktur der Datenbank / Speicherdatei zu erraten. Wenn er die Strucktur herausgefunden hat, kann er die Benutzereingabe so gestalten, dass neue oder andere Datensätze eingetragen werden. Es können auch Daten entfernt werden. Je nachdem wie viel der Angreifer weiss, kann er sogar die gesamte Datenbank zerstören. 

Beispiel: Folgende Daten werden als Variabeln in das SQL Skript eingefügt:

```
username = Joel
password = 12345678
isAdmin = 0
```

So sieht es im Java Code aus:

```Java
INSERT INTO user (useranme, password, isadmin) VALUES (
\"" + username + "\", \"" + password + "\" ,\"" + isAdmin + "\");
```

So wird es von SQL interpretiert:

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
'Joel','12345678','0');
```

username und password werden über ein Eingabefeld eingegeben. isAdmin ist im Benutzerobjekt gespeichert und wird so abgerufen. Sobald dies der Angreifer weiss, kann er folgendes in die Eingabefelder eingeben, um einen Adminaccount zu erstellen:

```
username: "Hacklord7000"
password: "meinPassword', 1); --"
```

Dies würde von SQL so interpretiert werden:

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
'Hacklord7000','meinPassword', 1); --, 0);
```

Der übrige SQL Code wird einfach asukommentiert. 

Wenn der Angreifer weiss, dass die Tabelle user heisst, kann er die ganze Tabelle löschen, indem er folgendes in die Eingebefelder eingibt: 

```
Username: "Hacklord7000"
Password: "meinPassword', 1); DROP TABLE user;--"
```

Dies würde von SQL so interpretiert werden:

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
'Hacklord7000','meinPassword', 1);
DROP TABLE user; --, 0);
```

Wieder wird der restliche SQL Code einfach auskommentiert.

Um dem entgegenzuwirken gibt es "Prepared Statements". Diese sorgen dafür, dass SQL weiss, was Anweisungen und was Daten sind. Die Variabeln werden durch Fragezeichen ersetzt, um danach mit einer "Prepared Statement Klasse" befüllt zu werden. 

Das SQL Skript würde so aussehen:

```SQL
INSERT INTO user (useranme, password, isadmin) VALUES (
?, ?, ?);
```

Ein Beispiel aus einem Lernatelier Projekt, wo wir (Delia, Melanie und ich) mit Springboot die "Prepared Statements" verwendet haben. 
//Bild einfügen 

## Verifikation
Anhand der Beschreibung oben und der Beispiele kann man sehen, dass ich verstanden habe wie "Interpreter Injections" funktionieren. Insbesondere "SQL Injections". 

# Reflektion zum Arbeitsprozess
Wie "Interpreter Injections" funktionieren, habe ich schnell begriffen. Auch die theoretischen Aufgaben dazu konnte ich ohne Schwierigkeiten lösen. Insbesondere liefen die Angriffsaufgaben gut. Problematischer wurde es, als es darum ging die "Injections" zu verhindern. Für unser Lernatelier Projekt mussten wir "Prepared Statements" machen, um unsere Datenbank zu schützen. Da Springboot anders funktioniert als JSF, musste ich mich zuerst einlesen. Dies dauerte eine Weile. Wie man sich vor XML Injections schützen kann, habe ich noch nicht verstanden. 


Um meine Applikationen auch gegen XML Injections zu schützen, werde ich mich darin einlesen, sobald ich es benötige. 
