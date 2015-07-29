[Home](home)  
[Wiki](WikiSolidus)  

### public void run()
  
Da die Initialisierung der Roboter am Cup nicht so durchführbar war wie geplant, mussten wir die Initialisierung anpassen. Dies führte dazu, dass die Roboter direkt nebeneinander in der Einfahrtsschneise zum Spielfeld stehen. Damit die Robotinos während des Einfahrens nicht auf den Abstand der Banden reagieren, da sie sonst mit dem anderen Robotinos kollidieren würden, wird im WayAnalyzer die avoidingDetector Methode erst aufgerufen wenn der y Wert der aktuellen Position positiv ist.
  
### public void setAvoidspeedLeft(int disObstacle, double angle) und setAvoidspeedRight(int disObstacle, double angle)
  
Die Distanz zum Hindernis wurde zu Beginn statisch verglichen. Dies geschah mit Hilfe von parametrierbaren Distanzen.
Während der Diplomarbeit, wurden die statischen Distanz-Vergleiche durch mathematische Formeln ersetzt. Dadurch ist es möglich je nach Geschwindigkeit und Distanz zum Hindernis mit variablen Geschwindigkeiten in X- und Y-Richtung auszuweichen.
  
### public boolean checkLeftSide() und checkRightSide()

Diese Methoden wurden hinzugefügt um die linke und rechte Seite des Robotinos zu überprüfen. Sollte der Robotino rechts ausweichen wollen und sich ein Hindernis auf der Rechten Seite befindet wird die checkRightSide Methode ein True zurückgeben und somit weicht der Robotino auf die linke Seite aus. Um entscheiden zu können ob sich ein Hindernis auf einer Seite befindet oder nicht werden die Laserdaten mit einem parametrierbaren Wert verglichen. Sobald mehrere Werte kleiner sind als der parametrierte Wert gibt die Methode ein True zurück.
  
### public void infraredSensoring()
  
Die Infrarotsensoren stoppen den Robotino nicht mehr. Im Gegenteil, jetzt wenn ein Wert eines Infrarotsensors die Sicherheitsdistanz unterschreitet wird eine Geschwindigkeit gesetzt um die Distanz wieder zu vergrössern. Da dies jetzt eine Ausweichfunktion ist befindet sich diese Methode nun im WayAnalyzer.
  
### public void messageArrived(String string, MqttMessage mm)
  
Da in der Formel zur Berechnung der Ausweichgeschwindigkeit die aktuelle Geschwindigkeit benötigt wird muss diese zuerst von der messageArrived Methode empfangen werden. Die Nachricht wird in ein Speed Objekt gecastet und kann somit weiterverwendet werden.
  
### public void run()

Damit der Robotino während der Produktion zwischen den verschiedenen Positionen an der CS oder RS unterscheiden kann wird der approach Befehl mit einer Zahl über den Broker gegeben. Der Robotino Berechnet danach die Position und fährt dort hin.
  
### public void calcInOutCoord()
  
Inbetriebnahme und korrektur der Berrechnungen
  
### public void calcActCoord()
  
Erneurung der Position um Resolverabweichungen zu korrigieren
