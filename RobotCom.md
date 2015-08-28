[Home](home)  
[Back](WikiSolidus) 

------------------

# RobotCom
Diese Klasse verbindet das Java Programm mit dem Robotino. Dies wird benötigt um jegliche Informationen / Befehle mit dem Robotino auszutauschen. Die Verbindung wird wie folgt aufgebaut:
Importbereich
```
importcomm.RobotCom;
```
Variablenbereich
```
private RobotComcom;
```
Konstruktor
```
com = new RobotCom();
com.setAddress("127.0.0.1");
com.connectToServer();
```

Dieser Codeabschnitt muss nur einmal pro .jar Datei programmiert werden. Die Verbindung zu Robotino besteht danach auch in allen anderen Klassen.

## Variablenbereich
Die com Variable wird als RobotCom für diese Klasse definiert.

## Konstruktor
Mit dem "newRobotCom" Befehl wird der Konstruktor der RobotCom aufgerufen. Dieser startet danach einen Executor Service innerhalb der Klasse der die ProcessEvent() Methode in einem gewissen Zeitabstand aufruft.
Der setAddress("127.0.0.1") Befehl definiert die IP Adresse auf welche zugegriffen wird. Wird das Programm auf dem Robotino selbst ausgeführt, so muss die Localhost Adresse (127.0.0.1) eingegeben werden. Befindet sich aber das Programm auf einem separaten PC, so muss die IP Adresse des Robotinos eingegeben werden.
Die connectToServer() Methode verbindet schlussendlich das Java Programm mit dem Robotino. Nun können die Odometrie Daten und Befehle an den Omnidrive übergeben werden.

## ProcessEvent
Die processEventsMethode ist eine, von der API2, mitgelieferte Methode, die alle aktuellen Daten des Robotinos ausliest und danach, wenn nötig, die entsprechenden Methoden aufruft. In unserem Programm haben wir "nur" eine Methode benötigt, die regelmässig Daten vom Robotino empfangen muss. Diese ist die readingsEvent und befindet sich im PositionController.
