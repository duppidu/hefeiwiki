

## WayAnalyzer  
  
### public WayAnalyzer()
  

  
### public void run()
  
Da die Initialisierung der Roboter am Cup nicht so durchführbar war wie geplant, mussten wir die Initialisierung anpassen. Dies führte dazu, dass die Roboter direkt nebeneinander in der Einfahrtsschneise zum Spielfeld stehen. Damit die Roboter beim Einfahren in das Spielfeld nicht probieren auszuweichen, wird abgefragt ob er sich über der Position „0“ auf der Y-Achse befindet. Die Schneisen befinden sich unter Null auf der Y-Achse.
Um das Ausweichen in dieser Situation zu gewährleisten, wird der Aufruf der Methode „avoidingDetector() auf eine positive Y-Position überprüft.
  
### public void avoidingDetector()
  
### public void setAvoidspeedLeft(int disObstacle, double angle)
  
Erweiterung von Ausweichegeschwindigkeit x und y Achse
Die Distanz zum Hindernis wurde zu Beginn statisch verglichen. Dies geschah mit Hilfe von prametrierbaren Distanzen.
Während der Diplom Arbeit, wurden die statischen Distanz-Vergleiche durch mathematische Formeln ersetzt. Dadurch ist es möglich je nach Geschwindigkeit und der Nähe zum Objekt mit Variablen Geschwindigkeiten in X- und Y-Richtung auszuweichen.
  
### public void setAvoidspeedRight(int disObstacle, double angle)
  
Erweiterung von Ausweichegeschwindigkeit x und y Achse
Die Distanz zum Hindernis wurde zu Beginn statisch verglichen. Dies geschah mit Hilfe von prametrierbaren Distanzen.
Während der Diplom Arbeit, wurden die statischen Distanz-Vergleiche durch mathematische Formeln ersetzt. Dadurch ist es möglich je nach Geschwindigkeit und der Nähe zum Objekt mit Variablen Geschwindigkeiten in X- und Y-Richtung auszuweichen.
  
### public boolean checkLeftSide()
  
Methode wurde eingefügt um während dem ausweichen die linke Seite zu überwachen plus vergleich auf aktuelle Geschwindigkeit auf x Achse
  
### public boolean checkRightSide()
  
Methode wurde eingefügt um während dem ausweichen die linke Seite zu überwachen plus vergleich auf aktuelle Geschwindigkeit auf x Achse
  
### public boolean routeBlocked(int laserArrayPosition)
  

  
### public void infraredSensoring()
  
Durch erkennen eines Hindernisses wird in die Gegenrichtung ausgewichen, wurde wegen der Möglichkeit auszuweichen in WayAnalyzer umgetauscht
  
### public void messageArrived(String string, MqttMessage mm)
  
Wird benötigt um aktuelle Geschwindigkeit von dem Broker zu empfangen
  
## WayController  
  

  
### public WayController()
  

  
### public void run()
  
Erweiterungen der approach Methoden approach mit ÜBERGABEWERT 0  wird während Produktion und Exploration ander berechnungen nötig
  
### public void calcInOutCoord()
  
Inbetriebnahme und korrektur der Berrechnungen
  
### public void calcActCoord()
  
Erneurung der Position um Resolverabweichungen zu korrigieren
  
### public void messageArrived(String topic, MqttMessage message)
  

  
## CrashController  
  

  
