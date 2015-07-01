[Home](home) [Back](DokuSolidus)  
  
## Inhalt
  
- SoftwareTest
- HardwareTest
  
## LocalTest  

Der LocalTest beinhaltet das Testen der einzelnen Klassen Local auf dem PC.  
Gegebenenfalls schon mit dem MQTT Brocker.  
Dies wird fortlaufend und selbstständig durchgeführt. 

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| WayAnalyzer|avoidingDetector()|Gibt es die Richtige Koordinate zurück? Ändern der Robi Nummer (1,2,3) |X |
| WayAnalyzer|avoidLeft()|Übergabewerte statisch setzen mit sout kontrollieren ob In & Out der Maschine richtig gespeichert wurden |X |
| WayAnalyzer|avoidRight()| Übergabewert (Array) statisch setzen, mit sout testen ob jeder Array platz um eins nach hinten verschoben wurde|X |
| WayAnalyzer|routeBlocked|Alles über MQTT senden und über die Run Methode  die Funktionen `saveMachine()`,`handleexploCoords` & `jobHandler()` aufrufen  |X |
|WayController|calcInOutCoord() |Statischer Übergabewert festlegen(int), mit sout kontrollieren ob der richtige String zurückkommt |X|  
|WayController|messageArrived() |Statischer Übergabewert festlegen([Maschine](Machine)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) in der HMap gespeichert wurden |X|
|CrashController|crash() |Statischer Übergabewert festlegen(int & [Koordinaten](Coord)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) zurückkommt |X|
| CrashController| bumperControl()|Aufrufen der Funktion, mittels sout kontrollieren ob an den richtigen plätze das richtige gespeichert wurde |X|
| CrashController| infraredSonsoring()|Übergabewert(int) statisch festlegen(Produktenummer), mittels sout kontrollieren ob die Liste nach `initProdPlan` richtig zusammengestellt wurde|X|
| | ()| |X|
| | ()| |X|
| | ()| |X|
| | ()| |X|
gugus
----------

### SoftTest ###

Der SoftTes beinhaltet das Testen des Programmes auf dem Robotino.  
Die Methoden werden über die StateMachine aufgerufen.  
Dies ist der Realitätsnahster Test den wir bei uns ind der Schule durchführen können.  

----------

### HardTest ###

Der HardTest wird an dem SolidusCup vor Ort durchgeführt.  
Mit den richtigen MPS [Machinen](Machine), dem richtigen Spielfeld und der Originalen RefBox.  

----------