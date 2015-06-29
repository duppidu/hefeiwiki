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
| ExploControll|MQTT|Alles über MQTT senden und über die Run Methode  die Funktionen `saveMachine()` & `jobHandler()` aufrufen  |X |
|Machine| | ||
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