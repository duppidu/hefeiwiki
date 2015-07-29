[Home](home)  
[Wiki](WikiSolidus)  

Coord
===================

public Coord sub(Coord pos)
-----------
Rechnet die Differenz zwischen zweit Coord Klassen. z.B. coord1.sub(coord2) ==> coord1.x - coord2.x , coord1.y - coord2.y und coord1.phi - coord2.phi.

public calcAngle(Coord actual)
-----------
Berechnet aus der Positionsdifferenz (Zielposition - aktuelle Position) den Ausrichtungswinkel und gibt diesen anschliessend zurück. Diese wird für das Anfahren der neuen Position benötigt. Dafür wird das Winkelkoordinatensystem in folgende vier Quadranten aufgeteilt: Quadrant 1 (1° bis 89°), Quadrant 2 (91° bis 179°), Quadrant 3 (181° bis 269°) und Quadrant 4 (271° bis 359°) wobei die Fälle (0°, 90°, 180°, 270° und 360°) separat abgefangen sind.

public boolean inRangeXY(Coord actual, double toleranz)
-----------
Vergleicht ob sich der Robotino in der übergebenen Toleranz befindet. Es werden dabei nur die X und Y Werte berücksichtigt. Solange sich der Robotino ausserhalb desBereiches befindet wird ein False zurückgegeben.

public boolean inRangePhi(Coord actual, double toleranz)
-----------
Vergleicht ob sich der Robotino in der übergebenen Toleranz befindet. Es wird dabei nur der Winkel berücksichtigt Solange sich der Robotino ausserhalb des Bereiches befindet wird ein False zurückgegeben.

public boolean inRangePhi(Coord actual, double toleranz, double faktor)
-----------
Vergleicht ob sich der Robotino in der übergebenen Toleranz befindet. Es wird dabei nur der Winkel berücksichtigt. Die Toleranz wird bei dieser Methode mit einem Faktor multipliziert. Solange sich der Robotino ausserhalb des Bereiches befindet wird ein False zurückgegeben.





