[Home](home)  
[Wiki](WikiSolidus)  

-----------------

# Diagramme
## Klassendiagramm

![DriveGruppeDiagramm](https://gitlab.com/solidus/hefei/uploads/6e452bec5bc250d679caab5d702edafe/DriveGruppeDiagramm.PNG)  

Auf diesem Diagramm sind alle Klassen, die mit der Drive Gruppe zusammenhängen, abgebildet. Der WayAnalyzer scannt mittels Laser und Infrarotsensoren die Umgebung ab und übergibt der Drive Klasse falls nötig Ausweichgeschwindigkeiten mit. Falls der Robotino gegen einen Gegenstand fährt, so wird die CrashController Klasse das Signal des Bumpers auffangen und dieses dem WayController weitergeben, dieser ruft danach die stop Methode der Drive Klasse auf. 
Die Drive Klasse steuert den Omnidrive des Roboters an, so kann auf dem Feld verfahren werden. Damit das System weiss auf welchen Koordinaten der Roboter aktuell steht, wurde die PositionController Klasse programmiert. Diese berechnet laufend die Position des Robotinos mittels Drehgeber. Damit alle Klassen miteinander kommunizieren können, benötigen die Meisten die MqttComm-Klasse. Diese baut die Verbindung mit dem Broker auf.

## Sequenzdiagramme

### Ohne Crash oder Hindernis

![SequenceDrive](https://gitlab.com/solidus/hefei/uploads/a88c811ee44702082a32b2b4dd7c9c13/SequenceDrive.PNG)

Dieses Diagramm beschreibt die Art und Weise, wie die Kommunikation im Inneren der Drive Gruppe aufgebaut ist. Die Befehle kommen über den Broker bis zum WayController. Dieser wertet diese aus und ruft die entsprechende Methode der Drive Klasse auf. Sobald diese ein „True“ zurück gibt, wird eine entsprechende Nachricht auf den Broker gesendet.

### Mit Hindernis

![SequenceDriveAusweichen](https://gitlab.com/solidus/hefei/uploads/c42a9d751587d37f051edcc8854996d9/SequenceDriveAusweichen.PNG)

Wird während des Fahrens ein Hindernis auf der Strecke entdeckt, berechnet der WayAnalyzer die Ausweichgeschwindigkeit und gibt diese über den Broker dem Drive weiter. Diese wird durch das Drive verarbeitet und dem Omnidrive weitergeleitet.

### Mit Crash

![SequenceDriveCrash](https://gitlab.com/solidus/hefei/uploads/85a3b862a6710e6cde2e1fa43ce7833a/SequenceDriveCrash.PNG)

Wird aus einem Grund ein Crash mittels Bumper erkannt, wird der CrashController dem WayController dieses melden. Der WayController ruft dann unverzüglich die stop Methode des Drives auf. Wird der Bumper nicht mehr aktiviert, so ruft der WayController mit Hilfe des Auftrags-Case, die Methoden des Drives wieder auf.

