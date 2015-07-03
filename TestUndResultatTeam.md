[Home](home)   
[Back](DokuSolidus)   

***

### Testplan

**Situation:**  Die Kamera soll beim starten des Programms gestartet werden und nach erhalten des Startbefehles soll die Kameraerkennung gestartet werden.

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


### Resultat  

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