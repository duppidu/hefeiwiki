[Home](home)   
[Back](DokuSolidus)    
***
### Laserscanner
Die finalen Tests vor der Reise nach China waren sehr zuverlässig. Die Klasse Laserscanner kann folgendes:
- Vorhandene Linien extrahieren
- Linien nach Länge, Geradheit, Anzahl Punkte und Position filtern
- Array mit den 270 Laserwerten für andere Klassen zur Verfügung stellen
- Erkennen und melden, ob sich ein Objekt auf dem gesuchten Feld befindet
- Erkennen und melden, ob sich eine Maschine auf dem gesuchten Feld befindet
- Einen Anfahrpunkt vor der Maschine berechnen

Alle gesetzten Ziele wurden erreicht und zum Teil noch verbessert.
### StateMachine
Beim finalen Test vor China wurde folgendes festgestellt:
- Die Abläufe funktionieren richtig
- Die StateMachine handelt die Phasen und States richtig
- Gelegentlich bleibt ein Robotino stehen (Ursache nicht geklärt)
- Die Produktion ist nicht programmiert

Die gesetzten Ziele wurden erreicht.
### PositionSet
Das PositionSet mithilfe des Laserscanner funktioniert wie vorgesehen. Die Genauigkeit der gesetzten Position hat einen Fehlerbereich von +- 1cm. Die Robotinos setzen ihre Position sobald der vordere Robotino den Startbereich verlassen hat und fahren danach selber auf eine gesetzte Position auf dem Feld.