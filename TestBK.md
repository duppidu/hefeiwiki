[Home](home) [Back](DokuSolidus)  
  
## Inhalt
  
- SoftwareTest
- HardwareTest
  
## LocalTest  

Der LocalTest beinhaltet das Testen der einzelnen Klassen Local auf dem PC.  
Gegebenenfalls schon mit dem MQTT Brocker.  
Dies wird fortlaufend und selbstständig durchgeführt.
  
x = funktionstüchtig  
0 = Nicht geprüft  
f = funktioniert nicht, muss überarbeitet werden  
w = weggelassen

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| WayAnalyzer|LaserArray|Wird das LaserArray mit korrekten Werten gefüllt und aktualisiert |X |
| WayAnalyzer|avoidingDetector()|Die Zählung der ugültgen Werte muss gelöscht werden sobald ein Laserwert dazwischen gültig ist. So werden falsche Messungen annuliert|X |
| WayAnalyzer|avoidingDetector()|Die Winkel der Laserpositionen müssen korrekt bstimmt werden|X |
| WayAnalyzer|avoidingDetector()|Die kleinste ungültige Distanz muss in jedem Zyklus gespeichert werden|X |
| WayAnalyzer|avoidingDetector()|Es muss die korekte Ausweich-Meode aufgerufen werden sobald die Ausweichsprioritäten stegen|X |
| WayAnalyzer|avoidLeft()|Wird die Distanz und der Winkel des Lasers korrekt mitgegeben |X |
| WayAnalyzer|avoidLeft()| Entsprechend des mitgegebenen Laserwertes, müssen die Geschwindigkeiten entsprechend verändet werden (Nach links ausweichen und Vorfahrtgeschwindigkeit senken)|X |
| WayAnalyzer|avoidLeft()|Werden die errechnete Ausweichsgeschwindigkeiten per Broker an das "avoid" Topic übermittelt |X |
| WayAnalyzer|avoidRight()|Wird die Distanz und der Winkel des Lasers korrekt mitgegeben|X |
| WayAnalyzer|avoidRight()|Entsprechend des mitgegebenen Laserwertes, müssen die Geschwindigkeiten entsprechend verändet werden (Nach rehts ausweichen und Vorfahrtgeschwindigkeit senken)|X |
| WayAnalyzer|avoidRight()|Werden die errechnete Ausweichsgeschwindigkeiten per Broker an das "avoid" Topic übermittelt|X |
| WayAnalyzer|routeBlocked|Es muss in der vorgegeben Distanz ein Hindernis geziehlt abgefragt werden können  |0 |
|WayController|calcInOutCoord() | Es müssen von der Input Seite die Input- und die Outputkoordinaten berrechnte werden können |0|
|WayController|calcInOutCoord() | Es müssen von der Output Seite die Input- und die Outputkoordinaten berrechnte werden können |0|  
|WayController|calcInOutCoord() | Werden Koordinaten auf "input" und "Output" Topic gesendet |0|
|WayController|messageArrived() |Statischer Übergabewert festlegen([Maschine](Machine)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) in der HMap gespeichert wurden |X|
|CrashController|crash() |Statischer Übergabewert festlegen(int & [Koordinaten](Coord)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) zurückkommt |X|
| CrashController| bumperControl()|Aufrufen der Funktion, mittels sout kontrollieren ob an den richtigen plätze das richtige gespeichert wurde |X|
| CrashController| infraredSonsoring()|Übergabewert(int) statisch festlegen(Produktenummer), mittels sout kontrollieren ob die Liste nach `initProdPlan` richtig zusammengestellt wurde|X|
| | ()| |X|
| | ()| |X|
| | ()| |X|
| | ()| |X|


## SoftTest  

Der SoftTes beinhaltet das Testen des Programmes auf dem Robotino.  
Die Methoden werden über die StateMachine aufgerufen.  
Dies ist der Realitätsnahster Test den wir bei uns ind der Schule durchführen können.  

----------

### HardTest ###

Der HardTest wird an dem SolidusCup vor Ort durchgeführt.  
Mit den richtigen MPS [Machinen](Machine), dem richtigen Spielfeld und der Originalen RefBox.  

----------