[Home](home)  
[Wiki](WikiSolidus)  

## Klassendiagramm

![DriveGruppeDiagramm](https://gitlab.com/solidus/hefei/uploads/6e452bec5bc250d679caab5d702edafe/DriveGruppeDiagramm.PNG)  

Auf diesem Diagramm sind alle Klassen die mit der Drive Gruppe zusammenhängen abgebildet. Der WayAnalyzer scannt mittels Laser und Infrarotsensoren die Umgebung ab und übergibt der Drive Klasse falls nötig Ausweichgeschwindigkeiten mit. Falls der Robotino gegen einen Gegenstand fährt so wird die CrashController Klasse das Signal des Bumpers auffangen und dieses dem WayController weitergeben. Die Drive Klasse steuert den Omnidrive damit der Robotino fahren kann. Es ist sehr wichtig zu wissen wo sich Robotino befindet. Aus diesem Grund wurde die Positioncontroller Klasse programmiert. Diese berechnet laufend die Position des Robotinos mittels Drehgeber. Damit alle Klassen miteinander kommunizieren können brauchen einige auch noch die MqttComm klasse. Diese baut die Verbindung mit dem Broker auf.
