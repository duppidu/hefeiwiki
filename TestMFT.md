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

### ColorDetection

Der Test der ColorDetection wurde während des gesamten Explorationsablaufes vor der Reise nach China getestet. Vor des Tests mussten die Detektierung erst Kalibriert werden. Die Detektierung wurde an 5 Lampen getestet und wir kamen zu folgendem Resultat:  
- Kamera wird richtig gestartet  
- Farbdetektierung hat in 4 von 5 Fällen richtige Farbsäule erkannt    
- Lampenobjekt wurde richtig an den Broker gesendet  
- ColorDetection wird beendet und der Prozess des seperaten .jars wird geschlossen  
- Kamera wird ausgeschalten    

Das Testergebniss war zufriedenstellend. In China muss darauf geachtet werden das die Farbdetektierung den Lichtverhältnissen angepasst werden muss und nach Kalibriert werden muss.  