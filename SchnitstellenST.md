[Home](home)   
[Back](KonzeptST)   

***

## Thomas  

Die einzige Schnittstelle zu dem restliche Programm läuft über den Broker. Über diesen wird das Programm gestartet und am ende der Überprüfung ein Lampen-Objekt übermittelt.

##  Simon

###  MarkerCoordinates:

Da die Marker-Erkennung mithilfe einer Kamera funktioniert, besteht eine Schnittstelle zur Hardware des Systems(Robotino). Ansonsten besteht nur noch eine Schnittstelle zur Drive Klasse. Diese instanziert die MarkerCoordinates Klasse und kontrolliert das Programm.

###  ServoControl:

Die ServoControl Klasse besitzt mehrere Schnittstellen. Zum einen besitzt sie ebenfalls eine Verbindung zur Hardware des Systems, da sie über einen USB Anschluss den ServoBrick ansteuern muss. Zum Anderen besitzt sie eine Verbindung zum MQTT Broker. Die Steuerung der Servos geschieht über Befehle, die die Klasse über ein Topic des MQTT Broker erhält.
