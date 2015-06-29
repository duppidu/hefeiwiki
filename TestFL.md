[Home](home) [Back](DokuSolidus)  

----------

### Inhalt ###
- LocalTest
- SoftTest
- HardTest

----------

### LocalTest ###

Der LocalTest beinhaltet das Testen der einzelnen Klassen Local auf dem PC.  
Gegebenenfalls schon mit dem MQTT Brocker.  
Dies wird fortlaufend und selbstständig durchgeführt. 

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| ExploControll|jobHandler()|Gibt es die Richtige Koordinate zurück? Ändern der Robi Nummer (1,2,3) |X |
| ExploControll|saveMachine()|Übergabewerte statisch setzen mit sout kontrollieren ob In & Out der Maschine richtig gespeichert wurden |X |
| ExploControll|handleexploCoords()| | |
| ExploControll|MQTT|Alles über MQTT senden und über die Run Methode  die Funktionen `saveMachine()`,`handleexploCoords` & `jobHandler()` aufrufen  |X |
|Machine|idToName() |Statischer Übergabewert festlegen(int), mit sout kontrollieren ob der richtige String zurückkommt |X|  
|Machine|fill() |Statischer Übergabewert festlegen([Maschine](Machine)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) in der HMap gespeichert wurden |X|
|Machine|machineSecondSideGenerator() |Statischer Übergabewert festlegen(int & [Koordinaten](Coord)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) zurückkommt |X|
| ProductAssembly| | ||
| ProductControllLocal||||
| ProductControllMain| |||
| Zones||||
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