## WayController  
Der WayController steuert die den ganzen Fahrablauf. Er kommuniziert via Broker mit der State-Machine, von dieser werden die Aufträge an den WayController abgegeben. Zudem berrechnet er die Anfahrtspunkte Input- und Outputseitig der MPS welche via Broker vom ExploController abgespeichert.
  
## public WayController()  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml-File und weist diese den Variabeln zu.  
Ausgelesen werden die Distanz zu der Maschine welche angefahren werden muss und die Distanz von Input-Anfahrpunkt zum Output-Anfahrtpunkt.  
Es werden die Driveklasse, die WayAnalyzerklasse, die LaserScannerklasse (wird Singelton) und die CrashControllerklasse insatnziert. Es wird ein Poolplatz  
des globalen Scheduler instanziert.
   
## public void run()  
Die run()-Methode wird vom Scheduler zyklisch alle 75 Millisekunden gezündet. Das Auftrags-Case fällt zu beginn sofort in den Wartezustand. Der Auftrag wird mit  jedem Ablauf gespeichert indem der Auftrags-String auf einen Memory-String zugewiesen wird. Sobald der Roboter einen Auftrag erhält wird von der ExploControll  oder vom ProductControllLocal per Broker die Zielkoordinaten  übermittelt. Diese werden mit der drive.setTarget()-Methode an die Driveklasse weitergegeben.  Sobald ein Auftrag anliegt, epmfängt der WayController via Broker einen Sring welcher im Auftrags-Case abgefragt wird und die entsprechende Methode Aufruft bis  diese erfüllt wird. Das Erfüllen des Auftrags wird mit einem Bool signalisert. Sobald die aufgerufene Methode des Drives, den Wert "true" zurückgibt, wird die   Meldung via Broker auf das entsprechende Topic gesendet. Anschliessend fällt das Case in den Wartezustand.  
  
## public void calcInOutCoord()  
Die calcInOutCoord()-Methode berrechnet die Input- und Outputanfahrtspunkte sobald sie aufgerufen wird. Die Berrechnungen decken sämtliche Positionen wie die Maschine stehen kann ab. Die Methode benötigt das Wissen ob sie auf der In - oder der Output Seite steht.  
Sobald der Roboter die Maschine angefahen hat, wird der Methode mitgeteilt ob er auf der Input oder Output-Seite ist. Anschliessend werden die  Anfahrtskoordinaten, welche 50cm von der Maschine entfernt sind berrechnet. Jenachdem ob es ob der Roboter auf auf Input- oder Output-Seite steht, werden an das entsprechende Topic die Anfahrtskoordinaten gesendet. Nachdem berrechnet die Methode den auf der Maschine gegenüberliegende Anfahrtspunkt. Auch diese Koordinaten werden anschliessend auf das entsprechende Topic gesendet.  
Um trigonometrisch immer die richtigen Distanzen auf der X- und der Y-Achse zu erhalten, sind vier rechenbediengungen Notwendig.  
  
Wenn die Maschine auf folgenden Winkeln steht:
  
-Zwischen 0° und 90°, Sinus und Cosinus positiv.  
-Zwischen 90° und 180°, Sinus positiv und Cosinus negativ. Vertausch nach Goniometrie von Sinus und Cosinus Funktion zu horizontaler und vertikaler Geraden  
-Zwischen 180° und 270°, Sinus und Cosinus negativ.   
-Zwischen 270° und 360°, Sinus negativ und Cosinus positiv. Vertausch nach Goniometrie von Sinus und Cosinus Funktion zu horizontaler und vertikaler Geraden   
  
![trigo](https://gitlab.com/solidus/hefei/uploads/94f695987bd4ca1c240bd6e08b8cf1a5/trigo.jpg)  
  
## public void connectionLost(Throwable thrwbl)  
Gibt eine Exception aus, sobald die Verbindung mit dem Broker verloren geht.  
  
## public void messageArrived(String topic, MqttMessage message)  
Empfang-Methode von Broker. In dieser Methode wird überprüft ob auf den korrekten Topics  Meldungen erscheinen.  
Auf dem Topic Target werden die Zielkoordinaten als Coord-Klasse empfangen.  
Auf dem Topic Actions wird der Auftrag als String empfangen.  
  
## public synchronized void deliveryComplete(IMqttDeliveryToken imdt)  
Meldet dem Broker, dass die Nachricht empfangen wurde.
