[Home](home)  
[Wiki](WikiSolidus)  

## WayAnalyzer  
  
Der WayAnalyzer erkennt mit Hilfe des Lasers ob Hindernisse im Weg sind. Er berechnet eine Schneise, welche zum Zielpunkt reicht.  
Diese Schneise wird nun bis Hin zum Zielpunkt auf Hindernisse überprüft. Dies geschieht zyklisch.  
wird nun ein Hindernis erkannt, wird überprüft ob sich das Hindernis mehr auf der rechten Seite befindet oder auf der linken Seite.
Auf jene Seite auf welcher weniger Hindernispunkte liegen wird ausgewichen bis keine Punkte mehr vorhanden sind. 

  
  
![WayAnalyzerFlowChart](https://gitlab.com/solidus/hefei/uploads/e4ca2986f7aa3470cca39c53ceac1a53/WayAnalyzerFlowChart.jpg) 
  
## public WayAnalyzer()
  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml und dem staticDistanceParams.xml-File und weist diese den Variabeln zu. Aus dem drive.xml- file wird die Höchstgeschwindigkeit und die Infrarot-Mindestdistanzen ausgelesen. Aus dem staticDistanceParams.xml-File wird die Verzögerungs- und Ausweichedistanz und die Banden-Offsette ausgelesen. Zudem werden die Anzahl der Laserpunkte welche Nacheinander ungültig sein müssen festgelegt und die Schneisenbreite eingelesen.
  
## public void run()  
  
In der run()-Methode werden zyklisch die Laserwerte von 0° bis 270° eingelesen, der Weg bis zum Ziel wird errechnet und aktualisiert, und die aktuellen Koordinaten werden eingelesen. Ausserdem wird die avoidingDetector()-Methode aufgerufen welche die Schneise überprüft. Die run()-Methode wird alle 50 Millisekunden gezündet.  
  
![LaserArray](https://gitlab.com/solidus/hefei/uploads/51cc28feda4f1219ae5d6efe309c7889/LaserArray.jpg)  
Auf der Graphik ist der Range des Lasersensors abgebildet. Es wird veranschaulicht von welchen physikalischen Positionen das Array mit Laserwerten befüllt ist. 
  
## public void avoidingDetector()  
  
Der avoidingDetector() geht in einer while-Schlaufe für die linke Seite die Positionen vom 91° bis 180° und für die rechte Seite die Positionen 0° bis 89° durch.
Die Schlaufen beinhalten ein einen Vergleichs-Algorythmus welche der kleinste Laserwert speichert, sofern dieser nicht den Wert 0 aufweist. Dieser Wert wird dann übergeben, sobald ausgewichen werden muss. In den Schlaufen wird als nächstes Überprüft ob sich ein Hindernis in der Schneise befindet. Sobald der Laser nacheinander mehr ungültige Werte enthält als vorgegeben sind wird die Ausweiche-Priorität um einen Punkt erhöht. Diese Überwachung ist benötigt, um ungültige Werte auszufiltern. Wenn die Ausweichspriorität auf einer Seite auf höher oder gleich 1 ist wird ausgewichen.  
Sollten beide Seiten Hindernis-Prioritäten aufweisen, hat jene mit dem höheren Wert Priorität.  
  
![Fahrschneise](https://gitlab.com/solidus/hefei/uploads/b8def5cc5948997301d36a09770d5fa6/Fahrschneise.jpg)  
Die der Parameter aus dem staticDistanceParam.xml-File ist halb so gross wie die Verfahrschneise des Robotinos. die Rechte Seite wird von 0° aus bis 89° durchgeabeitet und mit Hilfe von Trigonometrie auf die Breite der halben Schneise überprüft. Die Linke Seite wird von 91° bis 180° auf die selbe weise überprüft. Dies wurde so gelöst, damit der Roboter nicht seitwärts auf die selben Distanzen reagiert wie auf jene welche Frontal auf ihn treffen.  
  
Sobald auf eine Seite ausgewichen werden muss, wird überprüft ob sich der Roboter weit genug zu der Bande entfernt befindet um in diese Richtung auszuweichen. Es wird überprüft mit Hilfe der checkLeft- und checkRightSide()-Methoden ob sich in der auszuweichenden Richtung kein anderes Objekt aufhält.
Wenn Weniger Hindernisse aufeinander Detektiert werden als vorgegeben wird der Zähler wieder auf 0 gesetzt. Zusätzlich darf der Robotino nicht nach auf eine andere Seite ausweichen, wenn bereits ein Hindernis in der Schneise detektiert worden ist und daher schon eine Ausweichsrichtung gegeben wurde.
  
  
![AusweichsSituationen](https://gitlab.com/solidus/hefei/uploads/775de6a7d063e9d24b93477ef2481265/AusweichsSituationen.jpg)  
  
Diese Graphik visualisiert, wie sich der Robotino zwischen komplexen Objektanordnungen hindurch manövriert.  
  
![Routen](https://gitlab.com/solidus/hefei/uploads/306a7a149029c6c4239decf4f7198ace/Routen.jpg)  
  
Diese Graphik deckt sämtliche Maschinenanordnungen ab, wie diese am Rande des Spielfeldes stehen können. Damit der Robotino nicht aus dem Spielfeld fährt wurde eine verbotene Zone vor den Spielfeldenden designt. Der Roboter darf diese verbotene Zone befahren, aber er darf nicht gegen die Bande ausweichen, sollte er ein Hindernis detektieren.
Die Grösse der Abstände können im staticDistanceParams.xml-File parametriert werden.  
Blaue Rechtecke = MPS  
Rote Zone       = verbotene Zone  
  
Sobald die setAvoidspeedLeft()- oder setAvoidspeedRight()-Methode die Ausweichegeschwindigkeiten errechnet hat, wird verglichen ob sich seit dem letzten Zyklus die Geschwindigkeiten verändert haben.
Wenn sich diese Verändert haben, wird die Speed-Klasse per Broker auf das "avoidingSpeed"-Topic gesendet.
  
## public void setAvoidspeedLeft (int disObstacle, double angle)  
  
Die avoidLeft()-Methode wird aufgerufen, wenn auf der rechten Seite ein Hindernis detektiert wurde. Sie überprüft Ahnand des mitgegebenen Laserwertes und dessen Winkel, wie schnell ausgewichen werden muss. Desto höher das Hindernis ist, desto schneller wird nach links ausgewichen und die Vorwärtsgeschwindigkeit verzögert. Ist das Hindernis zu weit entfernt, werden die Geschwindigkeiten beibehalten.  
Die Ausweichsgeschwindigkeiten in X- und Y-Richtung werden von einer Formel errechnet. Diese Formel errechnet die Ausweichegeschwindigkeiten dynamisch und ist im drive.xml-File parametrierbar.
  
## public void setAvoidspeedRight (int disObstacle, double angle)
  
Die avoidLeft()-Methode wird aufgerufen, wenn auf der linken Seite ein Hindernis detektiert wurde. Sie überprüft Anhand des mitgegebenen Laserwertes und dessen Winkel, wie schnell ausgewichen werden muss. Desto höher das Hindernis ist, desto schneller wird nach rechts ausgewichen und die Vorwärtsgeschwindigkeit verzögert. Ist das Hindernis zu weit entfernt, werden die Geschwindigkeiten beibehalten.  
Die Ausweichsgeschwindigkeiten in X- und Y-Richtung werden von einer Formel errechnet. Diese Formel errechnet die Ausweichegeschwindigkeiten dynamisch und ist im drive.xml-File parametrierbar.
  
  
## checkLeftSide()  
  
Sobald der Robotino einem Objekt ausweicht bewegt sich dieser seitwärts. Um zu Überprüfen ob sich ein Objekt auf der linken Seite im Weg befindet wird die Methode checkLeftSide() verwendet. Die Überprüfung wird folgendermassen durch geführt: Sobald der Roboter Links ausweicht wird die Methode aufgerufen. Durch eine while-Schlaufe werden die Positionen 165° bis 195° fortlaufend auf einen im staticDistanceParams.xml-File parametrierbaren Wert verglichen. Sobald mehr als der parametrierte Wert aufeinanderfolgende unzulässige Laserwerte entdeckt werden, wird die Methode setAvoidspeedRight aufgerufen. Dieser Vergleichsalgorythmus basiert auf dem selben wie der avoidingDetector() ihn verwendet.  

![checkLeftSide](https://gitlab.com/solidus/hefei/uploads/a4a7ce30edadf7fa82bce4a2c923581c/checkLeftSide.jpg)  
Visualisierung wie der Robotino während des Ausweicheprozesses nach links, die linke Seite überwacht.
  
## checkRightSide()  
  
Sobald der Robotino einem Objekt ausweicht bewegt sich dieser seitwärts. Um zu Überprüfen ob sich ein Objekt auf der linken Seite im Weg befindet wird die Methode checkRightSide() verwendet. Die Überprüfung wird folgendermassen durchgeführt: Sobald der Roboter Links ausweicht wird die Methode aufgerufen. Durch eine while-Schlaufe werden die Positionen -15° bis 15° fortlaufend auf einen im staticDistanceParams.xml-File parametrierbaren Wert verglichen. Sobald mehr als der parametrierte Wert aufeinanderfolgende unzulässige Laserwerte entdeckt werden, wird die Methode setAvoidspeedLeft aufgerufen. Dieser Vergleichsalgorythmus basiert auf dem selben wie der avoidingDetector() ihn verwendet.  


![checkRightSide](https://gitlab.com/solidus/hefei/uploads/c0be0bb827687b76779b343bcf73f0d5/checkRightSide.jpg)  
Visualisierung wie der Robotino während des Ausweicheprozesses nach rechtss, die rechte Seite überwacht.
  
## public boolean routeBlocked(int laserArrayPosition, int distance)  
  
Die routeIsBlocked() Methode detektiert Anhand eines einzelnen Laserstrahls ob die gewünschte Route direkt frei ist oder nicht.  
Als Mitgabewert benötigt sie die Laserposition und dessen Vergleichsdistanz. Sie gibt "true" zurück, wenn auf die verlangte Distanz ein Hindernis vorliegt.
  
  
## public void infraredSensoring()  
  
Diese Methode, Überprüft ob der Roboter sich einem Objekt nähert oder sich ein Objekt dem Roboter nähert. Sobald ein Sensor einen ungültigen Wert aufweist, wird in die entgegengesetzte Richtung gefahren bis alle Werte wieder in einem gültigen Bereich stehen.
  
![InfraredSensoring](https://gitlab.com/solidus/hefei/uploads/23ce961af647471aeccb24bc0e90af83/InfraredSensoring.jpg)  
Die Graphik visualisiert, in welche Richtung der Robotino ausweicht wenn ein oder mehrere Infrarotsensoren einen ungültigen Wert aufweisen.  
Blauer Pfeil  = Fahrtrichtung  
Rote Strahlen = Infrarot-Sichtfeld


