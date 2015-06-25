[Back](wikisolidus)

# Laserscanner

Die Laserscanner-Klasse ist die Klasse, welche gebraucht wird für den Robotino.  
Sie braucht fast alle Klassen des EnvirementSensing-Packages.  
In ihr findet man die nötigen Methoden um mit dem Laser auf dem Robotino zu arbeiten. 
   
Eine wichtige Funktion der Laserscanner-Klasse ist es, eine Maschine zu erkennen  
und die Koordinaten für einen Punkt davor zu berechnen.
Eine Liste mit erkannten Linien wird dazu durch verschiedene Filter geschickt.  

| Filtername | Art | Funktion |  
| -------- | -------- | -------- |  
| MinNumberReflectionsFilter | Klasse | Filtert Linien aus, die aus weniger Punkten bestehen als vordefiniert. Siehe auch: [LineExtraction](LineExtraction) |  
| Längenfilter | Methode | Filtert Linien aus, die kürzer oder länger sind als einen bestimmten Längenranges |  
| Zonenfilter | Methode | Filtert Linien aus, deren Mittelpunkt sich nicht in der Zone befindet, in der gesucht wird. |   

## Zonenfilter
![Zonenfilter](https://gitlab.com/solidus/hefei/uploads/c5c3ed08a385eeb83627dfad3541a558/Zonenfilter.JPG)  
1. Der Robotino sucht in dem von der Refbox gemeldeten Feld nach einer Maschine.
2. Er erkennt zwei Maschinen, die in Frage kommen.
3. Mithilfe der Überprüfung ob der Mittelpunkt der erkannten Kante in der selben Zone ist, wie gesucht wird, wird die andere Maschine rausgefiltert.
