[Home](home)  
[Wiki](WikiSolidus)  

## WayController  
Der WayController steuert den ganzen Fahrablauf. Er kommuniziert via Broker mit der State-Machine, von dieser, werden die Aufträge an den WayController abgegeben. Er berechnet die Anfahrtspunkte der Input- und Outputseite der MPS. Die Anfahrtspunkte werden via Broker an den ExploController gesendet. Der ExploController speichert diese Punkt ab.
  
## public WayController()  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml-File und weist diese den entsprechenden Variabeln zu.  
Ausgelesen werden die Distanz zu der Maschine welche angefahren werden muss und die Distanz vom Input-Anfahrpunkt zum Output-Anfahrtpunkt.  
Es werden die Driveklasse, die WayAnalyzerklasse, die LaserScannerklasse (Singleton) und die CrashControllerklasse insatnziert. Es wird ein Poolplatz des globalen Scheduler instanziert.
   
## public void run()  
Die run()-Methode wird vom Scheduler zyklisch alle 75 Millisekunden gezündet. Das Auftrags-Case fällt zu Beginn sofort in den Wartezustand ("awaiting"). Sobald der Roboter einen Auftrag erhält, werden von der ExploControll-Klasse oder vom ProductControll-Klasse per Broker die Zielkoordinaten  übermittelt. Diese werden mit der drive.setTarget()-Methode an die Driveklasse weitergegeben. Sobald ein Auftrag anliegt, empfängt der WayController via Broker einen String, welcher im Auftrags-Case abgefragt wird und so die entsprechende Methode Aufruft. Das Erfüllen des Auftrags wird mit einem Bool signalisiert. Sobald die aufgerufene Methode des Drives, den Wert "true" zurückgibt, wird die   Meldung via Broker auf das entsprechende Topic gesendet. Anschliessend fällt das Case in den Wartezustand.  
  
## public void calcInOutCoord()  
Die calcInOutCoord()-Methode berechnet die Input- und Outputanfahrtspunkte sobald sie aufgerufen wird. Die Berechnungen decken sämtliche Positionen wie die Maschine stehen kann ab. Die Lampe ist immer an der Outputseite montiert.   
Sobald der Roboter die Maschine angefahren hat, wird die Berechnung des Outputseitigen Anfahrtspunktes gestartet. Die Anfahrtskoordinaten sind jeweils 50cm von der Maschine entfernt. Anschliessend berechnet die Methode anhand des bereits errechneten Outputanfahrtspunkt, den  gegenüberliegende Inputanfahrtspunkt. Die Koordinaten werden anschliessend auf das entsprechende Topic gesendet.  
  
  
![OutputPointCalc](https://gitlab.com/solidus/hefei/uploads/0a061bb62d836877e8d4117ab6c5a80b/OutputPointCalc.jpg)  
Auf der Grafik sind alle Situation vertreten welche die vier Quadranten abdecken. Der zu berechnende Punkt liegt auf dem Kreuz in der Mitte der Graphik. Der Punkt von welchem aus berechnet wird, ist jeweils die Spitze vor der MPS.  
Formel:  
Auf der Graphik ist ersichtlich wie die X- und Y-Achsendistanzen anhand der Hypotenuse errechnet werden.
Von den aktuellen Koordinaten werden die errechneten X- und Y-Distanzen subtrahiert. Den trigonometrischen Funktion ändert sich das Vorzeichen (+/-) je nach Quadrant und gewährleistet stets ein korrektes Resultat.  
      
![InputPointCalc](https://gitlab.com/solidus/hefei/uploads/4a6609e74a94a574c66c3de88134a24c/InputPointCalc.jpg)  
Der zu errechnende Punkt liegt ebenfalls auf dem Kreuz in der Mitte der Graphik. Der Ausgangspunkt wird von den grünen Robotinos dargestellt. Die Pfeile stellen die Blickrichtungen dar.  
Formel:  
Auf der Graphik ist ersichtlich wie die X- und Y-Achsendistanzen anhand der Hypotenuse errechnet werden. Da sich der Winkel des Robotino um 180° wendet, wird wenn der Robotino grösser gleich 180° steht Phi minus 180° gerechnet und wenn Phi kleiner ist als 180° wird plus 180° gerechnet.
Von den errechneten Output-Koordinaten werden die errechneten X- und Y-Distanzen addiert. Den trigonometrischen Funktion ändert sich das Vorzeichen (+/-) je nach Quadrant und gewährleistet stets ein korrektes Resultat.
  
## public void calcActCoord()  
  
Die Methode besteht grundsätzlich aus der selben Berechnungsformel, welche die Methode calcInOutCoord() nutzt um den Output-Anfahrtspunkt zu berechnen. Der Unterschied liegt daran, dass der Robotino je länger er fährt desto ungenauer die Drehgeber-Werte werden. Diese Methode wird während der Produktionsphase verwendet, um dem Roboter die Koordinaten neu zu setzen und so grosse Abweichungen zu verhindern.  
Die Methode berechnet sobald der Roboter sich vor der Maschine befindet, auf welcher Position er jetzt stehen muss unabhängig der Resolverwerte. Dazu benötigt er die Koordinaten, welche während der Explorationsphase durch die calcInOutCoord()-Methode errechnet und aufgenommen wurden. Diese Koordinaten werden trigonometrisch verrechnet und der Roboter erhält wieder genauere Positionen.
  
## public void connectionLost(Throwable thrwbl)  
Gibt eine Exception aus, sobald die Verbindung mit dem Broker verloren geht.  
  
## public void messageArrived(String topic, MqttMessage message)  
Empfang-Methode von Broker. In dieser Methode wird überprüft ob auf den korrekten Topics  Meldungen erscheinen.   
Auf dem Topic Target werden die Zielkoordinaten als Coord-Klasse empfangen.  
Auf dem Topic Actions wird der Auftrag als String empfangen. Der Auftrag wird mit  jedem Ablauf gespeichert indem der Auftrags-String auf einen Memory-String zugewiesen wird.  
Auf dem Topic Phase, wird die Spielphase als String empfangen.
  
## public synchronized void deliveryComplete(IMqttDeliveryToken imdt)  
Meldet dem Broker, dass die Nachricht empfangen wurde.


