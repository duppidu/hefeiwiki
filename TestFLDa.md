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
|MPS|idToName() |Statischer Übergabewert festlegen(int), mit sout kontrollieren ob der richtige String zurückkommt |X|  
|MPS|fill() |Statischer Übergabewert festlegen([MPS](MPS)), mit sout kontrollieren ob die richtigen [MPS](MPS) in der HMap gespeichert wurden |X|
|MPS|machineSecondSideGenerator() |Statischer Übergabewert festlegen(int & [Koordinaten](Coord)), mit sout kontrollieren ob die richtigen [MPS](MPS) zurückkommt |X|
| ProductAssembly| initProdPlan()|Aufrufen der Funktion, mittels sout kontrollieren ob an den richtigen plätze das richtige gespeichert wurde |X|
| ProductControllLocal|initAssignement()|Übergabewert(int) statisch festlegen(Produktenummer), mittels sout kontrollieren ob die Liste nach `initProdPlan` richtig zusammengestellt wurde|X|
| ProductControllLocal|MQTT|Über das Main mittels Befehl "backwards" muss jedesmal eine [Koordinate](Coord) der entsprechenden [MPS](MPS) gesendet werden|X|  
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
|Explocontroll / Drive | Coords Senden | verarbeitet die Belegten Felder in [Koordinaten](Coord) und sendet diese entsprechend der Robot Nr. Weiter an den [Waycontroller](WayController) |X |
|Explocontroll / Drive| Coords erhalten | Input und Output [Koordinaten](Coord) vom Drive erhalten und in der Richtigen MPS Speichern| |
|Explocontroll / MarkerDetection| Tag ID erhalten | Tag ID erhalten und Speichern |X |
|Explocontroll / ColorDetection| Lampe erhalten | Lampe erhalten und speichern welche die jeweiligen Zustände(R, O, G) ausgibt |X |
|Explocontroll | MPS Speichern |Kontrollieren ob bei erhalt von Backwards die Vorder und Hinterseite der maschine korrekt gespeichert wurde | |
|Explocontroll / Drive | Neue Coords Senden | Weitere [Koordinate](Coord) senden um das 2te feld zu entdecken | |

Der Test wurde anhand des Sequenz Diagramms der [ExploCommunication](ExploCommunication) teilweise durchgeführt und abgehandelt
Leider konnten wir den Test noch nicht beenden. Wir mussten darauf warten, bis das ausweichen zuverlässig Funktionierte und befassten uns desshalb mit 
dem ausprogrammieren der Produktion. 

----------

### <a name="ht">HardTest</a> ###

Der HardTest wird an dem RoboCup vor Ort durchgeführt.  
Mit den richtigen MPS [Machinen](Machine), dem richtigen Spielfeld und der Originalen RefBox. 
   
| Klasse | Funktion | Beschreibung | I.O |
| :------- | --- | --- | :---- | 
| Refbox / ExploControllMain | Felder erhalten | Sendet die Belegten Felder von der Refbox an den ExplocontrollMain und verarbeitet diese weiter | X |  
| ExploControllMain / ExploControllLocal | Feld senden | erstes Feld senden um mit der Exploration zu beginnen | X |  
| StateMachine / ExploControllLocal | Freigabe erhalten | Freigabe senden, damit mit der Explorationsphase begonnen werden kann | X |  
| ExploControllLocal / Drive | Coords senden | verarbeitet das erhaltene Feld in [Koordinaten](Coord) und sendet diese weiter | X |  
| MarkerDetection / ExploControllLocal | Tag ID erhalten | Tag ID erhalten und speichern | X |  
| ColorDetection / ExploControllLocal | Lampe erhalten | Lampenobjekt mit dem aktuellen Zustand erhalten uns speichern | X |  
| ExploControllLocal | MPS speichern | Kontrolle ob auf den backwards befehl die gesammelten daten korrekt gespeichert werden | X |  
| ExploControllLocal | MPS Komplettieren | MPS über den Main Broker zu den anderen Robotinos senden zum Komplettieren der hashMap. | X |  
| ExploControllLocal / ExploControllMain | Job anfordern | Neuen Job anfordern bei der Klasse [ExploControllMain](ExploContollMain) und diesen korrekt in Coords umwandeln  | X |  
  
Am Robocup mussten wir noch die Position der Lampe ändern, da sich die Lampensäule am Output befand und nicht am Input. Dieser Fehler war dadurch aufgetreten, weil wir unserer logischen überlegung mehr Glauben schenkten als dem Regelbuch. Durch unsere Projektstruktur konnten wir den Fehler jedoch in Kurzer Zeit beheben. 
  
----------