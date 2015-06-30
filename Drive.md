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


## Decelerate

## Go to Target

## Approach

## Explore
![Treppensignal](https://gitlab.com/solidus/hefei/uploads/a70756c478f66f30390dd1396c457d3d/Treppensignal.PNG)
