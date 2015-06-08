ServoControl
===================

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| Host| private final String| Localhost für Anschluss via USB |
| Port| private final int| via USB -->4223 |
| UID| private String| ID des IMU-Brick |
| x, y, z, w | private float| Quaternionen der Achse x, y, z, w |
| degree, zAngle | private double| Hilfsvariable für die Berechnung des Winkels in Grad |
| rad | private double| Hilfsvariable für die Berechnung des Winkels in Rad |

public void setQuaternion()
-----------
Abfrage der Quaternionen in den Achsen x, y, z, w

public void getDegreeAngle()
-----------
Berechnen und Rückgabe des Winkels in Grad

public void getRadAngle()
-----------
Berechnen und Rückgabe des Winkels in Rad
