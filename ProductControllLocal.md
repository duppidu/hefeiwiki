### Inhalt ###
- initAssignement()



----------
### Allgemein ###



----------

### initAssignement() ###

- Übergabewert Produktnummer `int`
- Durchsuchen der Liste `product` in [initProdPlan()](ProductAssembly) nach nächster Maschine
- Rückgabewert [Coord](Coord) von nächster Maschinen Position

Var `prodStep` ist ein Zähler der die Produktionsschritte Zählt und garantiert, dass die richtigen [Coords](Coord) zurückgegeben werden.
Ist das Produckt abgeschlossen wird, `prodStep`= -1  und ein neues Produkt(Job) wird angefordert. 

----------
