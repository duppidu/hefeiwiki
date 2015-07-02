[Home](home)  
[DokuSolidus](DokuSolidus)  

---------------------

## WayAnalyzer
### CPU Auslastung

In einem ersten Schritt wurde die CPU Auslastung von 120% auf 15%-20% verringert. Um dies erreichen zu können haben wir die Berechnungen mit den Laserpunkten optimiert. Diese Berechnungen werden jetzt ein Mal durchgeführt und danach auf ein Variable geschrieben.

### Links oder rechts?

Damit der Robotino den einfacheren Weg nimmt wird als erstes das gesamte Blickfeld des Lasers berechnet und danach entschieden ob er sich nach links oder rechts bewegen muss. Dies konnte mit einem Zähler einfach realisiert werden, indem die Punkte auf der linken und rechten Seite gezählt werden und danach zusammen verglichen werden. Der Robotino weicht dann auf die Seite aus auf welcher sich weniger Störpunkte befinden.

### Geschwindigkeit

Die Geschwindigkeit wird mittels Laserwert bestimmt. Dieser wird mit 6 IF Vergleichen verglichen indem sich verschiedene X und Y Geschwindigkeiten befinden. Diese Methode ist leider noch statisch da die momentan die einfachste Möglichkeit ist diese Aufgabe zu lösen.

## Drive

### Optimierung

Durch Absprache mit dem Team wurde bei der goToTarget Methode die machineAlign Methode hinzugefügt damit diese automatisch durch das Drive aufgerufen wird. Die machineAlign und targetAlign Methode wurden zur Align Methode zusammengeführt. Der Grund dafür ist dass diese Methoden sehr ähnlich sind und durch wenige Änderungen zusammengeführt werden können. 

### Kommunikation

Die Kommunikation zwischen WayAnalyzer und Drive wurde mittels Speed Klasse realisiert. Diese wird vom WayAnalyzer geschrieben und dann über den Broker gesendet. Das Drive empfängt diese Klasse dann und überschreibt danach die eigenen Geschwindigkeiten.  
  
## WayController  
  
### Koordinatenberrechnung
  
Die Input und Outputkoordinaten werden durch trigonometrische Formeln errechnet. Damit die berechneten Koordinaten auf das richtige Topic gesendet werden muss die calcInOutCord() Methode wissen auf welcher Seite der MPS der Roboter steht.
  
## CrashController
  
### Bumper  
  
Der Bumper wird über die API2-Bibliothek ausgewertet und abgefragt.
  
### Infrarot  
  
Die InfrarotSensorer werden alle einzeln im Konstruktor instanziert und deren Nummern werden dort ebenfalls zugewiesen. Hindernisse werden problemlos erkannt.  Ursprünglich sollten die 9 Infrarotsensoren in einem Array instanziert werden. So konnten die Nummern und die Vergleiche schön und dynamisch in einer Schlaufe abgearbeitet werden. Leider gab es das Problem, dass der Scheduler-service auf diese Art abstürzte. Da die Zeit nicht mehr reicht und die Ressurcen besser genutzt werden können als diesen Fehler zu suchen, wurde entschieden die die Sensoren wieder einzeln zu instanzieren. 