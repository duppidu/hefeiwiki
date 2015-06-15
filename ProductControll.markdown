### Inhalt ###
- initAssignement()
- jobHandler()


----------
### Allgemein ###



----------

### initAssignement() ###

- Durchsuchen der Liste `product` in [initProdPlan()](ProductAssembly)

----------

### jobHandler() ###

- Sucht in der Liste `jobs`, den Job mit der höchsten Priorität aus.
- Rückgabewert = JobNummer (Integer)
- Löschen des Jobs aus der Aktuellen Liste

Die Priorität des Jobs wird durch die Herstell Schwierigkeit bestimmt.
Die einfachen Jobs werden zuerst abgearbeitet.

----------