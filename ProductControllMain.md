[Home](home) [Back](WikiSolidus)

### Inhalt ###

- jobHandler()
- Communication


----------
### Allgemein ###

Diese Klasse läuft separat auf einem Hauptrechner!  
Handelt die Produktionsphase von allen Robotinos.  
Sobald von einem Robi der Befehl [getJob](ProductControllLocal) eintrifft, wird aus der Liste `jobs` ein neuer Job ausgesucht und dieser dem Robotino gesendet.

----------

### jobHandler() ###

- Sucht in der Liste `jobs`, den Job mit der höchsten Priorität aus.
- Rückgabewert = JobNummer (Integer)
- Löschen des Jobs aus der Aktuellen Liste

Die Priorität des Jobs wird durch die Herstell Schwierigkeit bestimmt.
Die einfachen Jobs werden zuerst abgearbeitet.

----------

### Communication ###

Die Kommunikation wird mittels MQTT gewährleistet!  
Das UML beschreibt dies, mit den entsprechenden Pfaden und Inhalten.  


![ProduktionCom](https://gitlab.com/solidus/hefei/uploads/399e165f29bf71a49581d8893accdf12/ProduktionCom.PNG)  

----------
