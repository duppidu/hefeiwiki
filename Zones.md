[Home](home) [Back](WikiSolidus)



### Inhalt ###
 - Allgemein
 - Zones()
 - Zonen

----------

### Allgemein ###

Beinhaltet ein Array indem die Eckpunkte von allen Zonen abgespeichert sind.  
Die Koordinaten, die sich in der nähe der Bande befinden, sind mit einem Offset versehen,  
so dass der Robi nicht in die Bande fährt.  
Diese Koordinaten werden in der [Explorationsphase](ExploControll) verwendet.

----------

### Zones() ###

 - Mit `Zones()` können fix einprogrammierte Koordinaten auf dem Spielfeld angefahren werden.

 - `Zones()` beinhaltet ein Array von [Coord`s](Coord) .
 - Die [Koordinaten](Coord) entschprechen den Eckpunkte, der entsprechenden Zone inc einem OffSet Wert.


 - Array Platz = Feldnummer.
 - Rückgabewert = [Coord](Coord)



----------

### Zonen ###


![spielfeld](https://gitlab.com/solidus/hefei/uploads/9c16481551f1f62c1524b4e1deed6891/spielfeld.PNG)

----------
