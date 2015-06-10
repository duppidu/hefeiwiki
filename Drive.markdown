Drive
===================

Die Drive Klasse steuert "nur" die Bewegungen des Robotinos. Damit der Robotino ohne zu Stocken auf dem Spielfeld fährt müssen die gewünschten Methoden mindestens alle 100ms aufgerufen werden. Damit der Robotino genau verfahren kann muss diese Zeit kleiner sein, dies bewirkt aber ein Anstieg der CPU Belstung. Während den ersten Tests (POE 2015) wurde mit einer Zykluszeit von 50-75ms gearbeitet.

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| target| Private Coord| Beinhaltet die Ziel Position. Kann durch setTarget() geändert werden|
| actual| Private Coord| Beinhaltet die aktuelle Position des Robotinos.|
| avoidSpeed| Private Speed| Beinhaltet die Ausweichgeschwindigkeit des Robotinos.|
| goToTargetCase| Private String| Variable für Switch Case in der goToTarget() Methode.|
| exploreCase| Private String| Variable für Switch Case in der explore() Methode.|
| approachCase| Private String| Variable für Switch Case in der approach Methode.|
| topicActual| Private String| Topic Pfad für die aktuelle Position.|
| topicAvoidingSpeed| Private String| Topic Pfad für die Ausweichgeschwindigkeit.|
| toleranz| Private Static Double| Definiert die Genauigkeit, beim Verfahren in X und Y, des Robotinos auf dem Spielfeld.|
| rotationTol| Private Double| Definiert die Genauigkeit, beim Verfahren in Phi, des Robotinos. Langsames Fahren|
| rotationFac| Private Double| Definiert die Genauigkeit, beim Verfahren in Phi, des Robotinos. Schnelles Fahren|
| breakDistance| Private Double| Definiert ab welcher Distanz der Robotino bremsen muss damit er das Ziel nicht verfehlt.|
| maxSpeed| Private Float| Definiert die maximale Geschwindigkeit mit der der Robotino fahren darf.|
| xSpeed| Private Float| Geschwindigkeit in X Richtung.|
| ySpeed| Private Float| Geschwindigkeit in Y Richtung.|
| omega| Private Float| Winkelgeschwindigkeit|
| beschleunigung| Private Float| Bestimt die Steigung der Anfahrrampe.|
| aproachspeed| Private Float| Geschwindigkeit für das Anfahren der Objekte.|
| rotationSpeed| Private Float| Drehgeschwindigkeit für Winkelanpassungen.|
| bandDistX| Private Int| Distanz der X Bande vom Nullpunkt|
| bandDistY| Private Int| Distanz der Y Bande vom Nullpunkt|
| backcycle| Private Int| Aktuelle Anzahl der Rückwärtszyklen.|
| laserTol| Private Int| Toleranz zum Ausrichten mit dem Laser in mm.|
| cntDone| Private Int| Zählt die Zyklen welche der Robotino gerade steht.|
| explore| Private Int| Wird in Switch Case benötigt um zu entscheiden in welche Ecke der Robotino gehen muss.|


public Drive()
----------------
Der Konstruktor instanziert die Kommunikation zum MQTT Broker, den Omnidrive, den PositionController, den Laserscanner, den DistanceSensor und die Markerdetection. Der DistanceSensor Klasse wird mitgeteilt welcher Sensor bewacht werden muss.
Nachdem werden alle Daten aus der Drive.xml Datei gelesen und den dazugehörigen Attributen zugewiesen.
Die Verbindung zu MQTT Broker wird hergestellt. Dazu wird die robotIp der main.xml Datei verwendet. Als letztes wird das Callback auf die zwei Topics, topicActual und Topic AvoidîngSpeed, gesetzt.


public void setTarget()
----------------
Das nächste Ziel wird dem Drive übergeben. Im gleichen Schritt wird die Schrittkett auf "align" gesetzt damit der Robotino bei der goToTarget Methode von vorne beginnt.

public boolean backwards()
----------------
Der Robotino fährt während 10 Zyklen rückwärts. Diese Methode wird verwendet um von der Maschine weg zu kommen. Sobald die 10 Zyklen vorbei sind wird ein True zurückgegeben.

private boolean targetalign()
----------------
Die Methode targetAlign() berechnet den Winkel zwischen Ziel und aktueller Position. Zudem wird der Robotino in diese Richtung gedreht.
Dabei verfährt der Robotino mit zwei verschiedenen Geschwindigkeit damit das Ziel genau und schnell erreicht wird. Die höhere Geschwindigkeit ist 10 Mal grösser als die rotationSpeed. Die rotationTol bestimt die Toleranz die beim langsamen drehen erreicht wird. Diese wird durch den rotationFac Faktor für das schnelle Drehen vergrössert. Je kleiner diese Werte sind desto genauer fährt der Robotino. Damit der Robotino eine kleinere Toleranz erreichen kann muss die Zykluszeit schneller eingestellt werden. Dies bewirkt ein Ansteig der CPU Belastung.

public boolean machineAlign()
----------------
Die Methode machineAlign() basiert auf dem gleichen Prinzip wie die targetAlign() Methode. Der grosse Unterschied zwischen den beiden ist dass sich der Robotino nicht in Richtung des Zieles orientiert sondern an den Winkel der mit dem Ziel (target) geliefert wurde.

private boolean accelerate()
----------------
Die Beschleunigung wird bei jedem Aufruf zur aktuellen geschwindigkeit dazu addiert. Wird maxSpeed erreicht wird ein true zurückgegeben. 

private boolean travel()
----------------
Der Robotino fährt solange gerade aus bis er die breakDistance erreicht hat. Danach wird die Geschwindigkeit auf approachSpeed gesetzt.

public boolean decelerate()
----------------
Der Robotino fährt so lange bis er sich in der Angegebenen Toleranz befindet.

public boolean aproache()
----------------
Die approach Methode richtet den Robotino aus mittels Laseralign. Mittels Tagerkennung wird die Position des Tags erkannt und der Robotin fährt vos des Tag hin. Der Infrarot Sensor misst die Distanz zwischen MPS und Robotino.

public boolean goToTarget()
----------------
Die goToTarget steuert mittels Switch Case den Ablauf zwischen targetAlign(), accelerate(), travel(), decelerate() und machineAlign() so dass eine Methode nach der Anderen ausgeführt wird. Die targetAlign() Methode wird in jedem Schritt aufgerufen damit der Robotino allfällige abweichungen des Winkels nachkorrigieren kann.

public boolean laserAlign()
----------------
Comming soon... Johner bitte usfülle

public boolean initPos()
----------------
comming soon... Johner bitte usfülle

public String recognizeMachine()
----------------
comming soon... Johner bitte usfülle

public boolean explore() 
----------------
Die explore() Methode sucht Maschinen die im eigenen Felde stehen. Damit die Maschine auf jeden Fall erkannt wird werden im schlimsten Fall vier Punkte angefahren. Wird eine Maschine erkannt fährt der Robotino vor diese hin.

public void stop()
----------------
Wie der Name schon sagt werden die Bewegungen des Robotinos gestoppt. Zudem werden die Switch Case Variablen auf die erste Position gesetzt. Dies Verhindert einen Crash beim wieder Anfahren.

