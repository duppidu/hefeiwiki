Compass
===================

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| Host| private final String| Localhost für Anschluss via USB |
| Port| private final int| via USB -->4223 |
| UID| private String| ID des IMU-Brick |
| x, y, z, w | Private float| Quaternionen der Achse x, y, z, w |

public Coord()
-----------
Default Konstruktor.

public Coord(double x, double y, double phi)
-----------
Setzt die Koordinatenklasse auf die x, y und phi Werte die übergeben werden.

Getter
-----------
Für x, y und phi besteht je eine get Methode.

public Coord sub(Coord pos)
-----------
Rechnet die Differenz zwischen zweit Coord Klassen. z.B. coord1.sub(coord2) ==> coord1.x - coord2.x , coord1.y - coord2.y und coord1.phi - coord2.phi.

public calcAngle(Coord actual)
-----------
Berechnet aus der Positionsdifferenz (Zielposition - aktuelle Position) den Ausrichtungswinkel und gibt diesen anschliessend zurueck. Diese wird für das Anfahren der neuen Position benoetigt. Dafuer wird das Winkelkoordinatensystem in folgende vier Quadranten aufgeteilt: Quadrant 1 (1° bis 89°), Quadrant 2 (91° bis 179°), Quadrant 3 (181° bis 269°) und Quadrant 4 (271° bis 359°) wobei die Fälle (0°, 90°, 180°, 270° und 360°) separat abgefangen sind.

public boolean inRangeXY(Coord actual, double toleranz)
-----------
Vergleicht ob sich der Robotino in der übergebenen Toleranz befindet. Solange sich der Robotino auserhalb dieses Bereiches befindet wird ein False zurückgegeben.

public boolean inRangeXY(Coord actual, double toleranz, double faktor)
-----------
Vergleicht ob sich der Robotino in der übergebenen Toleranz befindet. Diese wird mit einem übergebenen Faktor multiplizierz. Solange sich der Robotino auserhalb dieses Bereiches befindet wird ein False zurückgegeben.

public boolean inTargetRange(Coord actual, double toleranz, double faktor)
------------
Wird speziell für das targetAlign verwendet.




