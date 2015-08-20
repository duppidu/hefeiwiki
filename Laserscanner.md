[Back](wikisolidus)  
[Home](home)  
***

# Laserscanner

Die Laserscanner-Klasse ist die Klasse, welche gebraucht wird für den Robotino.  
Sie braucht fast alle Klassen des Laser-Packages.  
In ihr findet man die nötigen Methoden um mit dem Laser auf dem Robotino zu arbeiten. 
   
Eine wichtige Funktion der Laserscanner-Klasse ist es, eine Maschine zu erkennen  
und die Koordinaten für einen Punkt davor zu berechnen.
Eine Liste mit erkannten Linien wird dazu durch verschiedene Filter geschickt.  

| Filtername | Art | Funktion |  
| -------- | -------- | -------- |  
| MinNumberReflectionsFilter | Klasse | Filtert Linien aus, die aus weniger Punkten bestehen als vordefiniert. Siehe auch: [LineExtraction](LineExtraction) |  
| Längenfilter | Methode | Filtert Linien aus, die kürzer oder länger sind als einen bestimmten Längenranges |  
| Zonenfilter | Methode | Filtert Linien aus, deren Mittelpunkt sich nicht in der Zone befindet, in der gesucht wird. |  
*** 
## Erkennen der korrekten Maschine
![Laserscanner_Ablauf](https://gitlab.com/solidus/hefei/uploads/c7b268c71b898ae86618c55099c2163c/Laserscanner_Ablauf.JPG)  
Dies ist der Ablauf der filter() Methode. Sie kann so erkennen, ob sich etwas im Feld befindet und ob es eine Maschine ist.
***
## Zonenfilter
![Zonenfilter](https://gitlab.com/solidus/hefei/uploads/c5c3ed08a385eeb83627dfad3541a558/Zonenfilter.JPG)  
1. Der Robotino sucht in dem von der Refbox gemeldeten Feld nach einer Maschine.
2. Er erkennt zwei Maschinen, die in Frage kommen.
3. Mithilfe der Überprüfung ob der Mittelpunkt der erkannten Kante in der selben Zone ist, wie gesucht wird, wird die andere Maschine rausgefiltert.

***

![Mittelpunkt](https://gitlab.com/solidus/hefei/uploads/e4533bfbe15334df738d41d9c2ab5bed/Mittelpunkt.JPG)  
Hier wird die Maschine nicht rausgefiltert, weil der Mittelpunkt sich noch in der Zone befindet.
***
## Koordinatenumrechnung
Siehe auch: [Wikipedia/Koordinatentransformation](https://de.wikipedia.org/wiki/Koordinatentransformation)  
  
Die Punkte (Anfahrpunkt, Mittelpunkt der Maschine), die berechnet wurden sind auf einem Koordinatenfeld bei welchem der Laserscanner der Nullpunkt bildet.  
Da der Punkt aber auf dem absoluten Koordinatenfeld gebraucht wird, muss der Punkt umgerechnet werden.
![Koordinatenumrechnung](https://gitlab.com/solidus/hefei/uploads/5a3c5468e2204352509efb44447cc7f3/Koordinatenumrechnung.JPG)  
Das ist der Zustand, den wir vor der Umrechnung haben.  
Zuerst wird der Winkel ausgeglichen, das heisst um 90 Grad gedreht.  
### Koordinatenrotation
Danach wird eine Koordinatenrotation vorgenommen mit folgender Formel:
![translation](https://gitlab.com/solidus/hefei/uploads/11610a35d510e83181e5cf3b74676d55/translation.JPG)  
### Koordinatentranslation
Wenn dann die beiden Koordinatenfelder die selbe Ausrichtung haben, muss der Punkt nur noch durch Koordinatentranslation verschoben werden.
![CoordinateTranslation](https://gitlab.com/solidus/hefei/uploads/1f7570ee45f0e1b8e86e3f993f3fe34d/CoordinateTranslation.png)
