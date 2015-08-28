[Home](home)  
[Wiki](WikiSolidus)  

-----------------

# Drive
Die Drive Klasse steuert "nur" die Bewegungen des Robotinos. Damit der Robotino ohne zu Stocken auf dem Spielfeld fährt, müssen die gewünschten Methoden mindestens alle 100ms aufgerufen werden. Damit der Robotino genau verfahren kann, muss diese Zeit kleiner sein, dies bewirkt aber ein Anstieg der CPU Belastung. Während der ersten Tests (POE 2015) wurde mit einer Zykluszeit von 50-75ms gearbeitet.

## Ablauf
Um ein Ziel schnell, genau und sicher anfahren zu können, haben wir als Team folgenden Ablauf festgesetzt:
1. Ausrichten
2. Anfahren
3. Fahren
4. Bremsen
5. Ausrichten

Dieser Ablauf wurde aus dem Grund gewählt, weil der Laserscanner nur den vorderen Bereich des Robotinos überwachen kann. Das heisst, es wird wenn möglich vermieden den Roboter rückwärtsfahren zu lassen, da das Risiko einer Kollision zu gross ist.

## Align
Beim Aufruf dieser Methode wird ein Ziel in Form einer Coord Klasse mitgeliefert. Die Differenz zwischen der Zielkoordinate und aktuellen Koordinate bestimmt die Drehrichtung. Befindet sich diese wischen 0° und 180° oder ist kleiner als -180°, so dreht sich der Robotino im Uhrzeigersinn andernfalls im Gegenuhrzeigersinn.
Damit der Robotino so schnell wie möglich und genau genug den gewünschten Winkel erreicht, wurde beschlossen zwei verschiedene Geschwindigkeiten zu nehmen. Überschreitet die Differenz zwischen dem Zielwinkel und aktuellen Winkel einen eingestellten Wert, verfährt der Robotino mit der zehnfachen Geschwindigkeit. Sobald der eingestellte Wert unterschritten wird, wird die Geschwindigkeit reduziert und somit ein genaueres Verfahren ermöglicht.

## Accelerate
Bei jedem Aufruf wird die Beschleunigung der aktuellen Geschwindigkeit dazu addiert. Dadurch entsteht ein Treppensignal, welches durch den Beschleunigungswert und durch die Zykluszeit verändert werden kann. Verkleinert man die Beschleunigung so wird das Treppensignal flacher. Jedoch dauert dieser Prozess länger und könnte Probleme verursachen.

![Treppensignal](https://gitlab.com/solidus/hefei/uploads/a70756c478f66f30390dd1396c457d3d/Treppensignal.PNG)

## Travel

Im travel() wird nur die Geschwindigkeit beibehalten und gewartet bis die Abbremszone erreicht wird. Sobald diese erreicht ist wird ein "true" zurückgegeben.

## Decelerate

Die Geschwindigkeit wird auf approach-Speed zurückgesetzt und sobald das Ziel erreicht wird werden die Antriebe ausgeschaltet.

## Go to Target

Das goToTarget ist ein wichtiger Bestandteil der Drive Klasse. Diese Methode steuert den Ablauf der einzelnen Methoden, welche aufgerufen werden um den Robotino zum Ziel zu führen. Die Abfolge die dabei aufgerufen wird ist folgende:
- align(Coord), richtet den Robotino in Richtung des Ziels aus.
- accelerate(), beschleunigt den Robotino in X Richtung (Vorwärts).
- travel(), der Robotino fährt in die Abbremszone.
- decelerate(), bremst und führt den Robotino bis zum Ziel.
- align(Coord), richtet den Robotino anhand der Zielkoordinaten aus.  

Beim ersten „align“ wird eine Koordinatenklasse mitgegeben, welche den Wert„0“ als X und Y Wert beinhaltet. Jedoch ist der Phi-Wert, jener welcher ausschlaggebend ist. Der Phi-Wert wurde ausgerechnet um das Ziel geradlinig anzufahren.
In den Schritten „accelerate“, „travel“ und „decelerate“ wird jeweils die „align“-Methode zusätzlich aufgerufen. Dies wird benötigt um die kleinen Abweichungen beim Drehen zu kompensieren.
Das zweite „align“ wird mit der Zielkoordinate aufgerufen damit sich der Robotino in die Richtung des Ziels dreht.



## Explore

Die Explore Methode wird benutzt um das Zusammenspiel zwischen Kantenerkennung und Drive zu steuern.

![ExploreUR](https://gitlab.com/solidus/hefei/uploads/d1f4d3e3bb906b955187853d0c5488b4/ExploreUR.PNG)  

Hat der Robotino ein Feld erreicht so wird die Kantenerkennung gestartet. Findet diese eine Kante, die nicht der Länge einer aktiven Seite entspricht, so wird dem Robotino ein neues Ziel gesetzt. Dieses befindet sich immer in der nächsten, noch nicht angefahrenen Ecke der aktuellen Zone.

![ExploreOR](https://gitlab.com/solidus/hefei/uploads/4ad5920fa2b7a82ca47369896dea784c/ExploreOR.PNG)  

Die Kantenerkennung scannt ein zweites Mal. Wird eine aktive Seite erkannt, so steuert die Drive-Klasse den Robotino vor diese hin.

![MPS](https://gitlab.com/solidus/hefei/uploads/ae8f360c933b75e8f3e166cb77549275/MPS.PNG)  

Sobald der Robotino vor der MPS steht, schickt diese Methode ein „True“ zurück und wird somit nicht mehr aufgerufen.

![next](https://gitlab.com/solidus/hefei/uploads/36ae58be68974affc10dff31e35d374d/next.PNG)  

Wird ein leeres Feld oder keine passende Kante in der letzten Ecke erkannt, wird ein "next" auf den Broker gesendet. Dies ist ein Aufruf an den Explocontroller, damit der Robotino ein neues Feld zum Entdecken erhält.

Die Erfahrungen an dem Robocup in Hefei brachten hervor, dass der Ablaufprozess der Exploration ohne weitere Komplikationen funktionierte. Um mehr Zeit sparen zu können, müsste einerseits der von der Kantenerkennung gegebene Punkt weiter von der MPS entfernt sein. Die zweite Methode um Zeit zu sparen wäre mit der Tagerkennung frühzeitig festzustellen, ob es sich bei der MPS um eine Output oder Input Seite handelt. Anschliessend kann direkt die richtige Seite angefahren werden.


## Approach

Die Approach Methode ist dafür zuständig, dass der Robotino vor das Band oder die vier verschiedenen Offset Positionen fährt. Dies wird durch den Laser, dem vorderen Infrarotsensor und der Kamera gesteuert. Der Laser wird benötigt um den Robotino rechtwinklig an der MPS auszurichten. Die Kamera positioniert den Robotino vor dem AR Tag, damit das Band geradewegs angefahren werden kann. Durch den Übergabewert wird bestimmt auf welche Position der Roboter fahren muss. Wird ein „0“ mitgegeben, so fährt der Robotino direkt vor das Band. Wird jedoch eine Zahl von 1 bis 4 mitgegeben, fährt der Robotino zuerst seitwärts bis er vor der Position steht. Der Infrarot Sensor misst den Abstand zwischen Robotino und MPS. Wir haben bewusst den Infrarotsensor und nicht den Laser gewählt, da die Laserdaten grössere Abweichungen aufweisen als die der Infrarot Sensoren.

![CSPositionen](https://gitlab.com/solidus/hefei/uploads/3d0c968f5dc95c71b784070992bcac95/CSPositionen.PNG)
![RSPositionen](https://gitlab.com/solidus/hefei/uploads/238c07724a4c79b227db8beb36ca21e4/RSPositionen.PNG)

## MessageArrived
In der messageArrived Methode kommen alle Nachrichten, welche auf dem Broker verschickt werden, an. Damit die Topics nicht vertauscht werden, wird jeder Algorithmus in einer„IF Bedingung“ aufgerufen. Diese Bedingung vergleicht das Topic der angekommenen Nachricht mit dem Ziel-Topic.
Beim Topic „Actual“ ist dieser Algorithmus sehr einfach. Das Objekt, das versendet wurde, wird in ein Coord Objekt gecastet und danach auf eine lokale Variable geschrieben.
Beim TopicAvoidingSpeed ist der Code etwas komplexer. Falls das goToTargetCase sich im "targeAlign" oder "machineAlign" befindet, werden die Nachrichten nicht beachtet. Sobald sich der Robotino vorwärts bewegt, werden die Nachrichten des WayAnalyzer beachtet. Sobald eine Geschwindigkeit übergeben wird, wird diese auf die lokalen Variablen geschrieben. Kommt jedoch eine Geschwindigkeit von 10f an, wird diese auf den Default Wert des aktuellen Status gesetzt.
