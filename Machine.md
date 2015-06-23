### Inhalt ###
 - Machine
- Allgemein
- idToName
- fill
- machineSecondSideGenerator


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
- Inhalt: [Machine](Machine)



----------

### idToName() ###

- Uebergabewert = Tag ID (int)
- Return = [Machine](Machine) Name (String)

Wandelt die Tag ID von der Maschine ihn ihren dazugehörigen Namen um.


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