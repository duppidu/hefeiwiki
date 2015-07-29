[Home](home)  
[Wiki](WikiSolidus)  

## WayController  
Der WayController steuert den ganzen Fahrablauf. Er kommuniziert via Broker mit der State-Machine, von dieser, werden die Aufträge an den WayController abgegeben. Zudem berechnet er die Anfahrtspunkte Input- und Outputseitig der MPS welche via Broker vom ExploController abgespeichert.
  
## public WayController()  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml-File und weist diese den Variabeln zu.  
Ausgelesen werden die Distanz zu der Maschine welche angefahren werden muss und die Distanz von Input-Anfahrpunkt zum Output-Anfahrtpunkt.  
Es werden die Driveklasse, die WayAnalyzerklasse, die LaserScannerklasse (wird Singleton) und die CrashControllerklasse insatnziert. Es wird ein Poolplatz  
des globalen Scheduler instanziert.
   
## public void run()  
Die run()-Methode wird vom Scheduler zyklisch alle 75 Millisekunden gezündet. Das Auftrags-Case fällt zu Beginn sofort in den Wartezustand. Der Auftrag wird mit  jedem Ablauf gespeichert indem der Auftrags-String auf einen Memory-String zugewiesen wird. Sobald der Roboter einen Auftrag erhält wird von der ExploControll  oder vom ProductControllLocal per Broker die Zielkoordinaten  übermittelt. Diese werden mit der drive.setTarget()-Methode an die Driveklasse weitergegeben.  Sobald ein Auftrag anliegt, empfängt der WayController via Broker einen String welcher im Auftrags-Case abgefragt wird und die entsprechende Methode Aufruft bis  diese erfüllt wird. Das Erfüllen des Auftrags wird mit einem Bool signalisiert. Sobald die aufgerufene Methode des Drives, den Wert "true" zurückgibt, wird die   Meldung via Broker auf das entsprechende Topic gesendet. Anschliessend fällt das Case in den Wartezustand.  
  
## public void calcInOutCoord()  
Die calcInOutCoord()-Methode berechnet die Input- und Outputanfahrtspunkte sobald sie aufgerufen wird. Die Berechnungen decken sämtliche Positionen wie die Maschine stehen kann ab. Die Methode benötigt das Wissen ob sie auf der In - oder der Output Seite steht.  
Sobald der Roboter die Maschine angefahren hat, wird der Methode mitgeteilt ob er auf der Input oder Output-Seite steht. Anschliessend werden die  Anfahrtskoordinaten, welche 50cm von der Maschine entfernt sind berechnet. Je nachdem ob es ob der Roboter auf Input- oder Output-Seite steht, werden an das entsprechende Topic die Anfahrtskoordinaten gesendet. Nachdem berechnet die Methode den auf der Maschine gegenüberliegende Anfahrtspunkt. Auch diese Koordinaten werden anschliessend auf das entsprechende Topic gesendet.  
Um trigonometrisch immer die richtigen Distanzen auf der X- und der Y-Achse zu erhalten, sind vier Rechenbedingungen Notwendig.  
  
Wenn die Maschine auf folgenden Winkeln steht:
  
  
![trigo](https://gitlab.com/solidus/hefei/uploads/94f695987bd4ca1c240bd6e08b8cf1a5/trigo.jpg)  
  
## public void calcActCoord()  
  
Die Methode besteht grundsätzlich aus den selben Berechnungsformeln, wie die Methode calcInOutCoord(). Der Unterschied liegt daran, dass der Robotino je länger er fährt umso ungenauer seine Positionsberechnungen. Diese Methode während der Produktionsphase verwendet um dem Roboter die Koordinaten neu zu setzen und zu grosse Abweichungen zu verhindern.  
Die Methode berechnet sobald der Roboter sich vor der Maschine befindet auf welcher Position er jetzt stehen muss unabhängig der Resolverwerte. Dazu benötigt er die Koordinaten, welche während der Explorationsphase durch die calcInOutCoord()-Methode errechnet und aufgenommen wurden. Diese Koordinaten werden trigonometrisch verrechnet und der Roboter erhält wieder genauere Positionen.
  
## public void connectionLost(Throwable thrwbl)  
Gibt eine Exception aus, sobald die Verbindung mit dem Broker verloren geht.  
  
## public void messageArrived(String topic, MqttMessage message)  
Empfang-Methode von Broker. In dieser Methode wird überprüft ob auf den korrekten Topics  Meldungen erscheinen.  
Auf dem Topic Target werden die Zielkoordinaten als Coord-Klasse empfangen.  
Auf dem Topic Actions wird der Auftrag als String empfangen.  
  
## public synchronized void deliveryComplete(IMqttDeliveryToken imdt)  
Meldet dem Broker, dass die Nachricht empfangen wurde.

