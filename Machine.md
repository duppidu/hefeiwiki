[Home](home) [Back](WikiSolidus)

### Inhalt ###
 - MPS
- Beschreibung
- Allgemein
- idToName
- fill
- machineSecondSideGenerator


----------

### Beschreibung ###

Zuständig für das speichern und Verwaltet neuer Maschinen.   
Weiste den erkannten ID`s den richtigen Maschinen Name zu. 

#### Umbenannt
Gegen Aussen mussten wir den Namen der Klasse nachträglich abändern, da bei der Kommunikation mit der Refbox bereits der Begriff Machine verwendet wird.
Somit konnten wir den nicht auch verwenden und haben uns für den Namen MPS.  
Aus diesem Grund kann noch der Begriff Machine vorkommen welcher jedoch gleichbedeutend mit MPS ist. 

----------
### Machine ###

Attribute
----------

| Name| Datentyp| Bemerkung| 
| :------- | --- | :---- |
| Koordinaten| [Coord](Coord)| Position auf einem Koordinatenfeld|
|ID| int| ID von dem AR Tag|
| Lampen| [Lamps](ColorDetection)| Zustand der Lampensäule|

----------

### Allgemein ###

 - HashMap (hmMachine)
- Key: [Machine](Machine) Name (String)
- Inhalt: [MPS](Machine)


----------

### idToName() ###

- Uebergabewert = Tag ID (int)
- Return = [MPS](Machine) Name (String)

Wandelt die Tag ID von der [MPS](Machine) ihn ihren dazugehörigen Namen um.


----------
### fill() ###

Uebergabewert = (id, [coord](Coord), [lamps](ColorDetection))

- Füllt die HashMap (hmMachine) mit den Uebergabewerten.
- Der Key wird mittels `idToName()`  selbstständig ermittelt und gesetzt.
- Sollte ein Key schon vergeben/vorhanden sein, wird er überschrieben und durch den neuen Wert ersetzt. 


----------

### machineSecondSideGenerator() ###

Die Funktion speichert nach dem Erkennen einer Input Seite von einer Maschine automatisch die Output Seite derselben Maschine bez sie wird generiert.

Uebergabewert = (id, secondCoord)

- Mittels Input Tag einer Maschine wird das dazugehörige Output Tag automatisch generiert.
- Speichern der Output Seite von einer Maschine in der HashMap (hmMachine)
- Lampen auf second Seite sind alle false!
- secondCoord sind die Koordinaten wo sich "Theoretisch" das Output Tag befindet.

----------