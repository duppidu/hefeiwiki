## WayController  
Der WayController steuert die den ganzen Fahrablauf. Er kommuniziert via Broker mit der State-Machine, von dieser werden die Aufträge an den WayController abgegeben. Zudem berrechnet er die Anfahrtspunkte Input- und Outputseitig der MPS welche via Broker vom ExploController abgespeichert.
  
## public WayController()  
Der Konstruktor instanziert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml-File und weist diese den Variabeln zu.  
Ausgelesen werden die Distanz zu der Maschine welche angefahren werden muss und die Distanz von Input-Anfahrpunkt zum Output-Anfahrtpunkt.  
Es werden die Driveklasse, die WayAnalyzerklasse, die LaserScannerklasse (wird Singelton) und die CrashControllerklasse insatnziert.  
  


