[Home](home)  
[Wiki](WikiSolidus)  

## Klassendiagramm

![DriveGruppeDiagramm](https://gitlab.com/solidus/hefei/uploads/6e452bec5bc250d679caab5d702edafe/DriveGruppeDiagramm.PNG)  

Auf diesem Diagramm sind alle Klassen die mit der Drive Gruppe zusammenhängen abgebildet. Der WayAnalyzer scannt mittels Laser und Infrarotsensoren die Umgebung ab und übergibt der Drive Klasse falls nötig Ausweichgeschwindigkeiten mit. Falls der Robotino gegen einen Gegenstand fährt so wird die CrashController Klasse das Signal des Bumpers auffangen und dieses dem WayController weitergeben. Die Drive Klasse steuert den Omnidrive damit der Robotino fahren kann. Es ist sehr wichtig zu wissen wo sich Robotino befindet. Aus diesem Grund wurde die Positioncontroller Klasse programmiert. Diese berechnet laufend die Position des Robotinos mittels Drehgeber. Damit alle Klassen miteinander kommunizieren können brauchen einige auch noch die MqttComm klasse. Diese baut die Verbindung mit dem Broker auf.

## Sequenzdiagramme

![SequenceDrive](https://gitlab.com/solidus/hefei/uploads/f3346af5bfde99c2a64eed493ebd8a8c/SequenceDrive.PNG)

Dieses Diagramm beschreibt die Art und Weise wie die Kommunikation im inneren des Drive Gruppe funktioniert. Die Befehle kommen über den Broker bis zum WayController. Dieser wertet diese aus und ruft die entsprechende Methode der Drive Klasse auf. Sobald diese ein True zurück gibt wird eine Nachricht auf den Broker gesendet.


![SequenceDriveAusweichen](https://gitlab.com/solidus/hefei/uploads/55ee9a23ebab9d4d84dd667d8f8fa6b4/SequenceDriveAusweichen.PNG)

Wird während des Fahrens ein Hindernis auf der Strecke entdeckt, berechnet der WayAnalyzer die Ausweichgeschwindigkeit und gibt diese über den Broker dem Drive weiter. Diese wird durch das Drive verarbeitet und dem Omnidrive weitergeleitet.

![SequenceDriveCrash](https://gitlab.com/solidus/hefei/uploads/83ce8e3bee05e863c48628f138d0fb72/SequenceDriveCrash.PNG)

Wird aus irgend einem Grund ein Crash erkannt, wird der CrashController dem WayController dieses melden. Der WayController ruft dann unverzüglich die stop Methode des Drives auf. Wird der Bumper nicht mehr aktiviert so ruft der WayController die Methoden des Drives wieder auf.
