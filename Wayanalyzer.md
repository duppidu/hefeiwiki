## WayAnalyzer  
  
Der WayAnalyzer erkennt mit Hilfe des Lasers ob Hindernisse im Weg sind. Er berechnet eine Schneise, welche von der Distanz her bis zum Zielpunkt reicht.  
Diese Schneise wird nun bis Hin zum Zielpunkt auf Hindernisse überprüft. Dies geschieht zyklisch.  
wird nun ein Hindernis erkennt, wird überprüft ob sich das Hindernis mehr auf der rechten Seite befindet oder auf der linken Seite.
Auf der Seite auf weniger Hindernispunkte liegen wird ausgewichen bis keine Punkte mehr vorhanden sind.  
  
## public WayAnalyzer()
  

  
## public void run()  
  
In der run()-Methode werden zyklisch die Laserwerte von 270° eingelesen, der Weg bis zum Ziel wird aktualisiert, und die aktuellen Koordinaten werden   eingelesen. Ausserdem wird die avoidingDetector()-Methode aufgerufen welche die Schneise überprüft. Die run()-Methode wird alle 50 Millisekunden gezündet.

## public void avoidingDetector()  


## public void avoidLeft(int disObstacle, double angle)  


## public void avoidLeft(int disObstacle, double angle)


## public boolean routeBlocked(int laserArrayPosition)