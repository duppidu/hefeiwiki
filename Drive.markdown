Drive
===================

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| target| Private Coord| Beinhaltet die Ziel Position. Kann durch setTarget() geändert werden|
| actual| Private Coord| Beinhaltet die aktuelle Position des Robotinos.|
| schrittkette| Private String| Variable für die goToTarget() Methode.|
| toleranz| Private Static Double| Definiert die Genauigkeit, beim Verfahren in X und Y, des Robotinos auf dem Spielfeld.|
| drehtoleranz| Private Double| Definiert die Genauigkeit, beim Verfahren in Phi, des Robotinos. Langsames Fahren|
| drehtolfaktor| Private Double| Definiert die Genauigkeit, beim Verfahren in Phi, des Robotinos. Schnelles Fahren|
| breakDistance| Private Double| Definiert ab welcher Distanz der Robotino bremsen muss damit er das Ziel nicht verfehlt.|
| maxSpeed| Private Float| Definiert die maximale Geschwindigkeit mit der der Robotino fahren darf.|
| xSpeed| Private Float| Geschwindigkeit in X Richtung.|
| ySpeed| Private Float| Geschwindigkeit in Y Richtung.|
| omega| Private Float| Winkelgeschwindigkeit|
| beschleunigung| Private Float| Bestimt die Steigung der Anfahrrampe.|
| aproachspeed| Private Float| Geschwindigkeit für das Anfahren der Objekte.|
| drehgesch| Private Float| Drehgeschwindigkeit für Winkelanpassungen.|
| bandDistX| Private Int|| Distanz der X Bande vom Nullpunkt|
| bandDistY| Private Int| Distanz der Y Bande vom Nullpunkt|


public Drive()
----------------
Der Konstruktor instanziert alle nötigen Attribute, schreibt die Attribute mit den Werten aus der Drive.xml Datei und setzt das Calltback für die aktuelle Position.

public void setTarget()
----------------
Das nächste Ziel wird dem Drive übergeben. Im gleichen Schritt wird die Schrittkett auf "align" gesetzt.

public boolean backwards()
----------------
Der Robotino fährt während 10 Zyklen rückwärts. Diese Methode wird verwendet um von der Maschine weg zu kommen. Sobald die 10 Zyklen vorbei sind wird ein True zurückgegeben.

private boolean targetalign()
----------------
Die Methode targetAlign() dreht den Robotino in die Richtung des Zieles.

public boolean machineAlign(Coord target)
----------------
Die Methode machineAlign(Coord target) dreht den Robotino ca. rechtwinklig zu MPS. Als Übergabewert wird die Coord Klasse der MPS benötigt.

private boolean accelerate()
----------------
Beinhaltet dan Algorithmus für die Anfahrrampe.

private boolean travel()
----------------
Fährt dem Robotino bis zur breakDistance in Richtung des Zieles.

public boolean laserAlign()
----------------
Comming soon...

public boolean initPos()
----------------
comming soon...

