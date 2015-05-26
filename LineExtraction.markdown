# Line Extracter
Implementiert als Douglas Peucker Algorithmus  
http://de.wikipedia.org/wiki/Douglas-Peucker-Algorithmus
## Tutorial
### 1. Step: Linien aus vorhandenen (!) Reflektionen extrahieren
- LineExtracter Objekt instanzieren
- Übergabe von Toleranz in Konstruktor
- Aufrufen extractLines()
- Extrahiert alle Linien, egal wie viele Reflektionen die Linie definieren (mind. 2)  
![lineExtracter](https://gitlab.com/solidus/hefei/uploads/98fcef996ae50b3e61b3c3cc94fcf0b0/lineExtracter.png)  
- Fasst Zusammengehörige Reflektionen (innerhalb Toleranz) zu einer Linie zusammen

### 2. Step: Filtern der Linien
- MinNumberReflectionsFilter Objekt instanzieren  
- Übergabe der minimalen Anzahl Reflektionen, welche eine Linie definieren sollen in Konstruktor  
- aufrufen filter()  
- gibt nur Linien zurück, die durch min. durch entsprechende Mindestanzahl von Reflektionen definiert ist  
![lineExtracter_gefiltert](https://gitlab.com/solidus/hefei/uploads/9ac70c55a23d50e3047565af0252065d/lineExtracter_gefiltert.png)  
(Hier z.B. Mindesanzahl Reflektionen = 3)
