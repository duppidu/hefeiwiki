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

***

![Mittelpunkt](https://gitlab.com/solidus/hefei/uploads/e4533bfbe15334df738d41d9c2ab5bed/Mittelpunkt.JPG)  
Hier wird die Maschine nicht rausgefiltert, weil der Mittelpunkt sich noch in der Zone befindet.

## Koordinatenumrechnung
Die Punkte (Anfahrpunkt, Mittelpunkt der Maschine), die berechnet wurden sind auf einem Koordinatenfeld bei welchem der Laserscanner der Nullpunkt bildet.  
Da der Punkt aber auf dem absoluten Koordinatenfeld gebraucht wird, muss der Punkt umgerechnet werden.
![Koordinatenumrechnung](https://gitlab.com/solidus/hefei/uploads/5a3c5468e2204352509efb44447cc7f3/Koordinatenumrechnung.JPG)  
Das ist der Zustand, den wir vor der Umrechnung haben.