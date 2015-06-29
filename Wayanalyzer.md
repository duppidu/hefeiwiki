## WayAnalyzer  
  
Der WayAnalyzer erkennt mit Hilfe des Lasers ob Hindernisse im Weg sind. Er berechnet eine Schneise, welche von der Distanz her bis zum Zielpunkt reicht.  
Diese Schneise wird nun bis Hin zum Zielpunkt auf Hindernisse überprüft. Dies geschieht zyklisch.  
wird nun ein Hindernis erkennt, wird überprüft ob sich das Hindernis mehr auf der rechten Seite befindet oder auf der linken Seite.
Auf der Seite auf weniger Hindernispunkte liegen wird ausgewichen bis keine Punkte mehr vorhanden sind.  
  
## public WayAnalyzer()
  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml und dem staticDistanceParams.xml-File und weist diese den Variabeln zu. Aus dem drive.xml- file wird die Höchstgeschwindigkeit ausgelesen und aus dem staticDistanceParams.xml-File werden die Verzögerungs- und Ausweichedistanzen ausgelesen. Zudem werden die Azahl der Laserpunkte welche Nacheinander ungültig sein müssen festgelegt und die Schneisenbreite eingelesen.
  
## public void run()  
  
In der run()-Methode werden zyklisch die Laserwerte von 270° eingelesen, der Weg bis zum Ziel wird aktualisiert, und die aktuellen Koordinaten werden   eingelesen. Ausserdem wird die avoidingDetector()-Methode aufgerufen welche die Schneise überprüft. Die run()-Methode wird alle 50 Millisekunden gezündet.

## public void avoidingDetector()  
  
Der avoidingDetector() geht in einer while-Schlaufe für die linke Seite die Positionen vom 91° bis 180° und für die rechte Seite die Positionen 0° bis 89° durch.
Die Schlaufe beinhaltet ein einen Vergleichs-Algorythmus welche der kleinste Laserwert speichert, sofern dieser nicht den Wert 0 aufweist. Dieser Wert wird dann übergeben, wenn ausgewichen werden muss. In der Schlaufe wird als nächstes Überprüft
  
## public void avoidLeft(int disObstacle, double angle)  
  

  
## public void avoidLeft(int disObstacle, double angle)
  

  
## public boolean routeBlocked(int laserArrayPosition)  
  
