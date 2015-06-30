## WayAnalyzer  
  
Der WayAnalyzer erkennt mit Hilfe des Lasers ob Hindernisse im Weg sind. Er berechnet eine Schneise, welche von der Distanz her bis zum Zielpunkt reicht.  
Diese Schneise wird nun bis Hin zum Zielpunkt auf Hindernisse überprüft. Dies geschieht zyklisch.  
wird nun ein Hindernis erkennt, wird überprüft ob sich das Hindernis mehr auf der rechten Seite befindet oder auf der linken Seite.
Auf der Seite auf weniger Hindernispunkte liegen wird ausgewichen bis keine Punkte mehr vorhanden sind.  
  
![FlowChart_WayAnalyzer](https://gitlab.com/solidus/hefei/uploads/08f9372eb12c4436aa8b3eeb85c117d9/FlowChart_WayAnalyzer.jpg)  
  
## public WayAnalyzer()
  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml und dem staticDistanceParams.xml-File und weist diese den Variabeln zu. Aus dem drive.xml- file wird die Höchstgeschwindigkeit ausgelesen und aus dem staticDistanceParams.xml-File werden die Verzögerungs- und Ausweichedistanzen ausgelesen. Zudem werden die Azahl der Laserpunkte welche Nacheinander ungültig sein müssen festgelegt und die Schneisenbreite eingelesen.
  
## public void run()  
  
In der run()-Methode werden zyklisch die Laserwerte von 270° eingelesen, der Weg bis zum Ziel wird aktualisiert, und die aktuellen Koordinaten werden   eingelesen. Ausserdem wird die avoidingDetector()-Methode aufgerufen welche die Schneise überprüft. Die run()-Methode wird alle 50 Millisekunden gezündet.

## public void avoidingDetector()  
  
Der avoidingDetector() geht in einer while-Schlaufe für die linke Seite die Positionen vom 91° bis 180° und für die rechte Seite die Positionen 0° bis 89° durch.
Die Schlaufen beinhalten ein einen Vergleichs-Algorythmus welche der kleinste Laserwert speichert, sofern dieser nicht den Wert 0 aufweist. Dieser Wert wird dann übergeben, wenn ausgewichen werden muss. In den Schlaufen wird als nächstes Überprüft ob sich ein Hindernis in der Schneise befindet. Sobald der Laser nacheinander mehr ungültige Werte enthält als vorgegeben sind wird die Ausweiche Priorität um einen Punkt erhöht. Wenn Weniger Hindernisse aufeinander Detektiert werden als vorgegeben wird der Zähler wieder auf 0 gesetzt.  
Diese Überwachung ist benötigt, um ungültige Werte auszufiltern. Wenn die Ausweichspriorität auf einer Seite auf höher oder gleich 1 ist wird ausgewichen.  
Sollten beide Seiten Hindernis-Prioritäten aufweisen, hat jene mit dem Höheren Wert Priorität.
  
## public void avoidLeft(int disObstacle, double angle)  
  
Die avoidLeft()-Methode wird aufgerufen, wenn auf der rechten Seite ein Hindernis detektiert wurde. Sie überprüft Ahnand des mitgegebenen Laserwertes und dessen Winkel, wie schnell ausgewichen werden muss. Desto nöher das Hindernis ist, desto schneller wird nach links ausgewichen und die Vorwärtsgeschwindigkeit verzögert.
Ist das Hindernis zu weit entfern, werden die Geschwindigkeiten beibehalten. Um die effektive Distanz zum Hindernis zu erhalten wird der Laserwert trigonometrisch mit dem Winkel verrechnet.
  
## public void avoidLeft(int disObstacle, double angle)
  
Die avoidLeft()-Methode wird aufgerufen, wenn auf der linken Seite ein Hindernis detektiert wurde. Sie überprüft Ahnand des mitgegebenen Laserwertes und dessen Winkel, wie schnell ausgewichen werden muss. Desto nöher das Hindernis ist, desto schneller wird nach rechts ausgewichen und die Vorwärtsgeschwindigkeit verzögert. Ist das Hindernis zu weit entfern, werden die Geschwindigkeiten beibehalten. Um die effektive Distanz zum Hindernis zu erhalten wird der Laserwert trigonometrisch mit dem Winkel verrechnet.
  
## public boolean routeBlocked(int laserArrayPosition, int distance)  
  
Die routeIsBlocked() Methode detektiert Anhand eines einzeln Laserstrahls ob die gewünschte Route direkt frei ist oder nicht.  
Als Mitgabewert benötigt sie die Laserposition und dessen Vergleichsdistanz. Sie gibt "true" zurück, wenn auf die verlangte Distanz ein Hindernis vorliegt.

