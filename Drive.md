# Drive
Die Drive Klasse steuert "nur" die Bewegungen des Robotinos. Damit der Robotino ohne zu Stocken auf dem Spielfeld fährt müssen die gewünschten Methoden mindestens alle 100ms aufgerufen werden. Damit der Robotino genau verfahren kann muss diese Zeit kleiner sein, dies bewirkt aber ein Anstieg der CPU Belstung. Während den ersten Tests (POE 2015) wurde mit einer Zykluszeit von 50-75ms gearbeitet.

## Ablauf
Um ein Ziel schnell, genau und sicher anfahren zu können haben wir als Team folgende Abfolge festgesetzt:
1. Ausrichten
2. Anfahren
3. Fahren
4. Bremsen
5. Ausrichten  
Dieser Ablauf wurde aus dem Grund gewählt, weil der Laserscanner nur den vorderen Bereich des Robotinos bewachen kann und somit dieser Nicht rückwärts vefahren darf.

## Align
Die Differenz zwischen der Zeilkoordinate und aktuellen Koordinate bestimt die Drehrichtung. Befindet sie sich diese zwischen 0° und 180° oder ist kleiner als -180° so dreht sich der Robotino im Uhrzeigersinn. Beträgt die Differenz mehr als 180° oder zwischen 0° und -180° so wäre der Weg im Uhrzeigersinn länger als der im Gegenuhrzeigersinn.

## Accelerate
Bei jedem Aufruf wird die Beschleunigung der aktuellen Geschwindigkeit dazu addiert. Dadurch entsteht ein Treppensignal, dass durch den Beschleunigungswert und Zykluszeit verändert werden kann. 

![Treppensignal](https://gitlab.com/solidus/hefei/uploads/a70756c478f66f30390dd1396c457d3d/Treppensignal.PNG)


## Travel

Im travel() wird nur die Geschwindigkeit beibehalten und gewartet bis die Abbremszone erreicht wird. Sobald diese erreicht wird wird ein "true" zurückgegeben.

## Decelerate

Die Geschwindigkeit wird auf approachSpeed zurückgesetzt. Sobald da Ziel erreicht wird werden die Antriebe ausgeschalten.

## Go to Target

Das goToTarget ist ein wichtiger Bestandteil der Drive Klasse. Diese Methode steuert de Ablauf der einzelnen Methoden die aufgerufen werden um den Robotino zum Ziel zu führen. Die Abfolge die dabei aufgerufen wird ist:
- Align, richtet den Robotino in Richtung des Ziels aus.
- Accelerate, beschleunigt den Robotino in X Richtung.
- Travel, der Robotino fährt in die Abbremszone.
- Decelerate, bremst und führt den Robotino bis zum Ziel.
- Align, richtet den Robotino anhand der Zielkoordinaten aus.  

Beim ersten Align wird eine Koordinatenklasse mitgegeben die 0 als X und Y Wert beinhaltet. Jedoch der Phi Wert ist der der ausgerechnet wurde um das Ziel geradlinig erreichen zu können.  
In den Schritten Accelerate, Travel und Decelerate wird jewils die Align Methode zusätzlich aufgerufen. Dies wird benötigt um die kleinen Abweichungen beim Drehen zu kompensieren.  
Das zweite Align wird mit der Zielkoordinate aufgerufen damit sich der Robotino in die Richtung des Ziels dreht.

## Explore

Die Explore Methode wird benutzt um das Zusammenspiel zwischen Kantenerkennung und Drive zu steuern. Hat der Robotino ein Feld erreicht so wird die Kantenerkennung gestartet. Wird eine Kante erkannt so fährt das Drive vor diese hin. Wird jedoch keine Kante erkannt so wird dem Drive automatisch ein neuse Ziel gesetzt und dort wird das ganze erneut gestartet.

## Approach

Die Approach Methode ist dafür zuständig dass der Robotino vor das Band fährt. Dies wird durch den Laser, den Infrarot Sensor und der Kamera gesteuert. Der Laser wird benötigt um den Robotino rechtwinklig an der MPS auszurichten. Die Kamera Positioniert den Robotino vor dem AR Tag damit das Band gerade angefahren werden kann. Der Infrarot Sensor misst den Abstand zwischen Robotino und MPS. Wird haben bewusst den Sensor und nicht den Laser gewählt da die Laserdaten grössere Abweichungen aufweisen die die der Infrarot Sensoren.