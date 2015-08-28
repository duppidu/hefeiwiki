[Home](home)  
[Wiki](WikiSolidus)  

----------------

# PositionController
Diese Klasse bildet die Schnittstelle zwischen der Odometrie des Robotinos und dem Broker. Die aktuelle Position wird zyklisch mit dem processEvents() ausgelesen und bei einer Änderung von 0.1mm oder 0.1° auf den Broker gesendet. Der Winkel wird beim Auslesen aus der Odometrie von Rad in Grad umgewandelt. Zudem wird der Winkel um 180° verschoben damit Winkel von 0° bis 360° entstehen und nicht von -180° bis 180°.
