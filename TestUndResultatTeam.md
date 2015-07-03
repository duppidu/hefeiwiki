[Home](home)   
[Back](DokuSolidus)   

***

## Testplan

**Situation:**  Eine Explophase mit der Erkennung von 2 Maschinen soll getestet werden.

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| Start-Up|programStartup()|Start-Up instanziert in einer Schrittkette die Color detection |X |
| ColorDetection|Colordetection()|Starten der Kamera |X |
| ColorDetection|Colordetection()|Verbinden zum Broker|X |
| ColorDetection|Colordetection()|Starten des Schedulers aus dem Scheduler-pool im Main |X |
| ColorDetection|run()|Scheduler dreht im Lehrlauf und wartet immer 1 sec|X |
| ColorDetection|messageArrived()|String mit dem Inhalt "start" kommt beim Broker an. Dadurch wird messageArrived() aufgerufen und diese Startet dan die überprüfung |X |
| ColorDetection|run()|Starten der Überprüfung durch zyklischen Aufruf von trackColor() und controll()|X |
| ColorDetection|controll()|startet nachdem jede Farbe 41 mal überprüft wurde lightAnalyse()|X |
| ColorDetection|lightAnalyse()|Auswerten der überpüften Farbe und abspeichern in das Lamp Objekt|X |
| ColorDetection|mqttSend()|Senden des Lamp Objekts an den Broker|X |
| ColorDetection|controll()|versetzt den Scheduler wider in den Leerlauf|X |


## Resultat  

Die ExplorationsPhase erwies sich als schwieriger als erst angenommen. Ende PM Kurs ist es uns jedoch möglich 2 Maschinen zu entdecken und diese abzuspeichern. 
Leider konnten wir nicht all unsere Ziele vom PM erfüllen da sich einige unerwartete Probleme auftraten. Beispielsweise das Ausweichen des Robotinos erwies sich als schwieriger als angenommen. Ebenfalls wurde die Problematik mit der Refbox noch nicht behoben.  
Das herstellen eines ersten Produktes war ein zu hohes Ziel und wird jetzt in der nächsten Projektphase der Diplomarbeit weiterverfolgt.

### Teilziele:
| Teilziel| Resultat |
| :------- | --- |
| Der Start-Up Fall muss ausprogrammiert sein.| Start-Up ist bis zum aktuellen Stand ausprogrammiert |
| Driveklassen müssen funktionstüchtig und fehlerfrei arbeiten | Sind ausprogrammiert |
| State-Machine muss funktionsbereit sein | State-Machine ist auf dem aktuellen Stand|
| Zentralbroker muss Kommunikation zwischen Robotinos ermöglichen | Zentraler Broker ist eingerichtet |
| Restart-Funktion um Java-Programm neu zu starten | Restart wurde noch nicht angegangen |
| Robotino mechanisch komplett mit Greifer und Lösung für Bauteil abgriff | Die Teile sind fertig gedruckt und zusammengesetzt |
| Jeder Programmteil muss über ein angemessenes Diagramm verfügen (Klassendiag, Sequencediag, etc…) | Jeder hat sein Diagramm erstellt|
| Cupvorbereitungen müssen getroffen sein (Packlisten, Materialisten, Finanzierungen, Impfungen) | Listen wurden erstellt und Abklärungen getroffen |
| Refbox muss funktionieren | Refbox ist noch nicht soweit |