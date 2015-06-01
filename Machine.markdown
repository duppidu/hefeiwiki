
 - Machine
- Allgemein
- idToName
- fill


----------
### Allgemein ###

 - Konstruktor Machine
- [Coord](Coord) 
- ID 
- [Lamps](ColorDetection)


 - HashMap
- Key: Machine Name (String)
- Inhalt: Machine



----------

### idToName() ###

- Uebergabewert = Tag ID (int)
- Return = Machine Name (String)

Wandelt die Tag ID von der Maschine ihn ihren dazugehörigen Namen um.


----------
### fill() ###

Uebergabewert = (id, [coord](Coord), [lamps](ColorDetection))

- Füllt die HashMap (hmMachine) mit den Uebergabewerten.
- Der Key wird mittels `idToName()`  selbstständig ermittelt und gesetzt.
- Sollte ein Key schon vergeben/vorhanden sein, wird er überschrieben und durch den neuen Wert ersetzt. 


----------
