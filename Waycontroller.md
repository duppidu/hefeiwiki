[Home](home)  
[Wiki](WikiSolidus)  

-------------------

# WayController
Der WayController ist das zentrale Element der Drive Gruppe. Die Aufgabe dieser Klasse besteht darin die Aufträge der Statemachine, die über den Broker empfangen werden, abzuarbeiten. Zusätzlich wird das Zusammenspiel zwischen Drive, CrashController und WayAnalyzer koordiniert. Die Anfahrtspunkte werden von dieser Klasse aus berechnet und zum Speichern auf den Broker gesendet.

## Konstruktor
Der Konstruktor instanziiert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml-File und weist diese den entsprechenden Variablen zu.
Ausgelesen werden die Distanz zu der Maschine, welche angefahren werden muss und die Distanz vom Input-Anfahrpunkt zum Output-Anfahrpunkt.
Es werden die Drive-, die WayAnalyze-, die LaserScanner- und die CrashController Klasse instanziiert.
Zuletzt wird aus dem Executor Service Pool des StartUps einen Scheduler im 75 Millisekunden Takt instanziiert.

## Run
Die run()-Methode wird vom Scheduler zyklisch alle 75 Millisekunden aufgerufen. Das Auftrags-Case fällt zu Beginn sofort in den Wartezustand („awaiting“). Sobald die Klasse einen Auftrag erhält, wird dieser solange bearbeitet bis die aufgerufenen Methoden den Wert „true“ zurückgeben oder ein neuer Auftrag empfangen wird. Diese Aufträge werden über den Broker in Form eines Strings empfangen. Dadurch wird das Switch Case in den entsprechenden Status/Auftrag gesetzt. Wird beim Aufruf einer Drive Methode ein true zurückgegeben, so wird eine Nachricht auf den Broker gesendet und der Status wird auf „awaiting“ gesetzt.

## CalcInOutCoord
Die calcInOutCoord Methode berechnet anhand der aktuellen Position die theoretischen Anfahrtspunkte für die beiden aktiven Seiten der MPS. Dabei spielt es keine Rolle in welchem Winkel die Station steht. Die Anfahrtspunkte werden immer 50 cm von der MPS entfernt gesetzt. Grund dafür ist der Schlupf der Antriebe. Somit kann ein Anfahrtspunkt problemlos „ungenau“ angefahren werden. Die„appraoch“ Methode der Drive Klasse positioniert mit Hilfe des Lasers anschliessend den Roboter vor der MPS.
Die Methode wird nur von der Outputseite der MPS aufgerufen werden, da sonst die beiden Seiten der Station vertauscht würden. Diese Methode wird ausschliesslich während der Explorationsphase aufgerufen, nachdem die Lampe erkannt wurde. 

![OutputPointCalc](https://gitlab.com/solidus/hefei/uploads/0a061bb62d836877e8d4117ab6c5a80b/OutputPointCalc.jpg)  
Auf der Grafik sind alle Situationen vertreten, welche sich über die vier Quadranten des Einheitskreises erstrecken. Der zu berechnende Punkt liegt auf dem Kreuz in der Mitte der Graphik. Der Punkt, von welchem aus berechnet wird, ist jeweils die Spitze vor der MPS. Nach diesem Prinzip werden die Zielkoordinaten des Roboters anhand der aktuellen Koordinaten berechnet.
Formel:
Auf der Graphik ist ersichtlich wie die X- und Y-Achsendistanzen anhand der trigonometrischen Formel berechnet werden.
Um den Anfahrtspunkt auf der Outputseite zu berechnen, werden die errechneten Werte von der aktuellen Position abgezogen.
Bei der Inputseite werden jedoch die berechneten Werte der aktuellen Position dazu addiert. Da die gegenüberliegende Position um 180° gedreht ist, muss der Winkel zusätzlich berechnet werden. Beträgt der aktuelle Winkel mehr als 180° werden diesem 180° abgezogen. Befindet sich der Wert jedoch im Bereich unter 180°, so werden ihm 180° addiert.

![InputPointCalc](https://gitlab.com/solidus/hefei/uploads/4a6609e74a94a574c66c3de88134a24c/InputPointCalc.jpg)
Diese Graphik visualisiert die Berechnungssituationen für die inputseitigen Koordinaten. Der zu errechnende Punkt liegt ebenfalls auf dem Kreuz in der Mitte der Graphik. Der Ausgangspunkt wird mit den grünen Robotinos dargestellt. Die Pfeile stellen die Ausrichtung dar.

## CalcActCoord

Die Methode besteht grundsätzlich aus derselben Berechnungsformel, welche die Methode calcInOutCoord() nutzt um den Output-Anfahrtspunkt zu berechnen. Der Unterschied liegt darin, dass der Robotino je länger er fährt, desto mehr Schlupf in der Drehgeberauswertung entsteht. Diese Methode wird während der Produktionsphase verwendet, um die Koordinaten des Roboters neu zu setzen und so Abweichungen zu verhindern.
Die Methode berechnet, sobald der Roboter sich vor der Maschine befindet, auf welcher Position er jetzt stehen müsste, unabhängig der Drehgeberwerte. Dazu benötigt er die Koordinaten, welche während der Explorationsphase durch die calcInOutCoord()-Methode errechnet und abgespeichert wurden. Diese Koordinaten werden nach Formel verrechnet und die Drehgeberwerte werden dabei aufgefrischt. Die Drehgeber können nach dieser Prozedur wieder mit korrekten Werten arbeiten.

## MessageArrived
Empfangs-Methode vom Broker. Da Nachrichten von mehreren Topics ankommen müssen die Algorithmen mit dem entsprechenden Topic Name aktiviert werden.
Auf dem Topic Target werden die Zielkoordinaten als Coord-Klasse empfangen und direkt der Drive Klasse übergeben.
Auf dem Topic Actions wird der Auftrag als String empfangen und auf die quest Variable geschrieben. Sobald der Auftrag erledigt ist wird „awaiting“ auf die quest Variable geschrieben.
Auf dem Topic Phase, wird die Spielphase als String empfangen.
