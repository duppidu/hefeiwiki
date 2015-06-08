ServoControl
===================

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| Host| private final String | Localhost für Anschluss via USB |
| Port| private final int| via USB -->4223 |
| UID| private String | ID des IMU-Brick |
| min/maxPulse | private int | steht im zusammenhang mit dem min/maxDegree |
| min/maxDegree | private int | einstellung für den Winkelbereich des Servos |
| Period | private int | default Wert von 19500 |
| open/closeAcceleration | private int | default Wert von 0xFFFF |
| open/closeVelocity | private int | default Wert 0xFFFF |
| servoNr | private int | Anschlussposition des Servos auf dem Print |
| pos| int | Wert für das öffnen und schliessen des Greifers |


public void openGripper()
-----------
Methode für das öffnen des Grippers. Öffnungsgrad wird übergeben.


public void closeGripper()
-----------
Methode für das schliessen des Grippers. Schliessungsgrad wird übergeben.
