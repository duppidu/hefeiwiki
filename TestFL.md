[Home](home) [Back](DokuSolidus)  

----------

### Inhalt ###
- <a href="#lt">LocalTest</a>
- <a href="#st">SoftTest</a>
- <a href="#ht">HardTest</a>

----------

### <a name="lt">LocalTest</a> ###

Der LocalTest beinhaltet das Testen der einzelnen Klassen Local auf dem PC.  
Gegebenenfalls schon mit dem MQTT Brocker.  
Dies wird fortlaufend und selbstständig durchgeführt. 

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| ExploControll|jobHandler()|Gibt es die Richtige Koordinate zurück? Ändern der Robi Nummer (1,2,3) |X |
| ExploControll|saveMachine()|Übergabewerte statisch setzen mit sout kontrollieren ob In & Out der Maschine richtig gespeichert wurden |X |
| ExploControll|handleexploCoords()| Übergabewert (Array) statisch setzen, mit sout testen ob jeder Array platz um eins nach hinten verschoben wurde|X |
| ExploControll|MQTT|Alles über MQTT senden und über die Run Methode  die Funktionen `saveMachine()`,`handleexploCoords` & `jobHandler()` aufrufen  |X |
|Machine|idToName() |Statischer Übergabewert festlegen(int), mit sout kontrollieren ob der richtige String zurückkommt |X|  
|Machine|fill() |Statischer Übergabewert festlegen([Maschine](Machine)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) in der HMap gespeichert wurden |X|
|Machine|machineSecondSideGenerator() |Statischer Übergabewert festlegen(int & [Koordinaten](Coord)), mit sout kontrollieren ob die richtigen [Maschinen](Machine) zurückkommt |X|
| ProductAssembly| initProdPlan()|Aufrufen der Funktion, mittels sout kontrollieren ob an den richtigen plätze das richtige gespeichert wurde |X|
| ProductControllLocal|initAssignement()|Übergabewert(int) statisch festlegen(Produktenummer), mittels sout kontrollieren ob die Liste nach `initProdPlan` richtig zusammengestellt wurde|X|
| ProductControllLocal|MQTT|Über das Main mittels Befehl "backwards" muss jedesmal eine [Koordinate](Coord) der entsprechenden [Maschine](Machine) gesendet werden|X|  
| ProductControllMain| jobHandler()|Statische Liste von Jobs einlesen, bei jedem Aufruf wird der kleinste Job zurückgegeben und gelöscht|X|
| ProductControllMain| MQTT|Über Main dem Brocker Robi Nummer senden. Bei empfangen `jobHandler` aufrufen und mit sout kontrollieren |X|
| Zones|Zones()|Mittels sout kontrollieren, ob bei dem Konstruktoraufruf die ArrayListe richtig gefüllt worden sind |X|
| Zones|zoneDedector()|Statischer Übergabewert[Koordinate](Coord) festlegen, kontrollieren ob der Rückgabe wert dem Richtigen Name entspricht |X|

----------

### <a name="st">SoftTest</a> ###

Der SoftTes beinhaltet das Testen des Programmes auf dem Robotino.  
Die Methoden werden über die StateMachine aufgerufen.  
Dies ist der Realitätsnahster Test den wir bei uns ind der Schule durchführen können.  

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
|Refbox / ExploControll|Felder Senden| Sendet die Belegten Felder von der Refbox an den Explocontroll|X |
|Explocontroll / Drive | Coords Senden | verarbeitet die Belegten Felder in Coords und sendet diese entsprechend der Robot Nr. Weiter |X |
|Explocontroll / MarkerDetection| Tag ID erhalten | Tag ID erhalten und Speichern |X |
|Explocontroll / ColorDetection| Lampe erhalten | Tag ID erhalten und Speichern |X |
|Explocontroll / Drive| Coords erhalten | Tag ID erhalten und Speichern |X |
----------

### <a name="ht">HardTest</a> ###

Der HardTest wird an dem SolidusCup vor Ort durchgeführt.  
Mit den richtigen MPS [Machinen](Machine), dem richtigen Spielfeld und der Originalen RefBox.  

----------