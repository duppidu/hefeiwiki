[Home](home) [Back](WikiSolidus)


### Inhalt ###
- initAssignement()



----------
### Allgemein ###

Handelt gesamte Interne ProductionsPhase.  
Dies bedeutet, der Robi hat von dem [Main Computer](ProductControllMain) einen Job erhalten, teilt diesen in geeignete Arbeitsschritte auf  
und verarbeitet mithilfe eigener Funktionen diesen Job.  
Sobald das [Drive](Drive) eine neue [Koordinaten](Coord) benötigt, wird diese Klasse die [Koordinaten](Coord) die zur Produktion notwendigen nächsten [Koordinaten](Coord) an den Broker senden.

----------

### initAssignement() ###

- Übergabewert Produktnummer `int`
- Durchsuchen der Liste `product` in [initProdPlan()](ProductAssembly) nach nächster [Maschine](Machine)
- Rückgabewert [Coord](Coord) von der Position der nächsten [Maschinen](Machine) 

Var `prodStep` ist ein Zähler der die Produktionsschritte Zählt und garantiert, dass die richtigen [Coords](Coord) zurückgegeben werden.
Ist das Produckt abgeschlossen, wird `prodStep`= -1  und ein neues Produkt(Job) wird angefordert. 

----------
