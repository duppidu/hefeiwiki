ServoControl
===================

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| Host| private final String | Localhost für Anschluss via USB |
| Port| private final in t| via USB -->4223 |
| UID| private String | ID des IMU-Brick |
| min/maxPulse | private int | |
| min/maxDegree | private int | |
| Period | private int | |
| open/closeAcceleration | private int | |
| open/closeVelocity | private int | |
| servoNr | private int | |


public void setQuaternion()
-----------
Abfrage der Quaternionen in den Achsen x, y, z, w

public void getDegreeAngle()
-----------
Berechnen und Rückgabe des Winkels in Grad

public void getRadAngle()
-----------
Berechnen und Rückgabe des Winkels in Rad
