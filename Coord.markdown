Coord
===================

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| x| Private Double| X Koordinate in m.|
| y| Private Double| Y Koordinate in m.|
| phi| Private Double| Phi Koordinate in Grad.|

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
Dästi bitte usfülle

public boolean inRangeXY(Coord actual, double toleranz)
-----------
Vergleicht ob sich der Robotino in der übergebenen Toleranz befindet. Solange sich der Robotino auserhalb dieses Bereiches befindet wird ein False zurückgegeben.





