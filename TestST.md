[Home](home)   
[Back](DokuSolidus)    

----------

## Thomas  

Der genau Ablauf der Colordetection ist hier zu finden:
[ColorDetection](ColorDetection)

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


## Simon

Der genau Ablauf der Markerdetection, Colordetection und ServoControl ist hier zu finden:
[Markerdetection & MarkerCoordinates](Markerdetection_Markercoordinates)
[Servo / Grippercontrol](ServoGripperControl)

### Testplan

**Situation:**  Das JavaProgramm soll gstartet werden, welches das C++ Programm startet und einen Marker detektieren soll. Nach dem detektieren soll die ID des Markers zum MQTT Broker gesendet werden.


| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| MarkerDetection|MarkerDetection()| Ruft init() auf|X |
| MarkerDetection|init()| Erstellt einen Thread im gemeinsamen threadpool und startet startDetection()|X |
| MarkerDetection|startDetection()| Startet C++ Programm|X |
| MarkerDetection|run()|Führt detection() aus solange Thread läuft|X |
| MarkerDetection|mqttSend()|Sendet die Tag ID zum MQTT Broker|X |
| MarkerDetection|terminateDetection()| Beendet C++ Prozess und JavaProgramm|X |


**Situation:**  Das JavaProgramm soll gstartet werden, welches dann das C++ Programm startet und die Position eines Marker detektieren soll. Nach dem detektieren soll die Position des Markers als Rückgabewert an die Drive Klasse gesendet werden.


| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| MarkerCoordinates|startCoordinateDetection()| Startet C++ Programm|X |
| MarkerCoordinates|coordinatesDetection()|Detektiert Marker und speichert Wert in Variable und gibt Wert als Rückgabewert aus|X |
| MarkerCoordinates|terminateCoordinateDetection()|Beendet C++ und Java Programm|X |

**Situation:**  Die Servos sollen über einen Befehl des MQTT Brokers geöffnet und geschlossen werden.


| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| ServoControl|setServoSettings()|Setzt Einstellungen für die Servos|X |
| ServoControl|initializeMqtt)|Generiert Verbindung zum MQTT (Callback)|X |
| ServoControl|messageArrived()|Überprüft das Topic auf die gewünschten Nachrichten|X |
| ServoControl|openGripper()|Bringt die Servos in die "offen" Stellung|X |
| ServoControl|closeGripper()|Bringt die Servos in die "geschlossen" Stellung|X |
