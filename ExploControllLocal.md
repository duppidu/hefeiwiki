[Home](home)  
[Wiki](WikiSolidus)  
  
 Inhalt:
    
 - <a href="#fe">Feldverwaltung und Spielstart</a>
 - <a href="#da">Datenerfassung und Verwaltung</a>
 - <a href="#ab">Ablauf</a>

## ExploControllLocal



Diese Klasse behandelt die Explorations-Phase des Spiels. Aufgerufen wird die Klasse von der State Machine. Die Klasse stellt im Ablauf der Explorationphase ein zentrales Kommunikationsglied zwischen
Refbox, Waycontroller StateMachine, Marker-, LampDetection und den Anderen
Die Feldvergabe wird von einer anderen Klasse gehandelt, welche, auf einem externen Pc Läuft. Zudem werden die Angefahrenen und erkannten MPS Daten gespeichert und Übermittelt.

### <a href="#fe">Feldverwaltung und Spielstart</a>
Die Feldverwaltung wird von der Klasse [ExploControllMain](ExploControllMain) übernommen. Zu Spielbeginn wird als erstes an jeden Robotino ein Feld zum erkunden gesendet und auf eine Freigabe von der Statemachine abgewartet. Ist die Freigabe erteilt, beginnt die Explorationsphase.

### <a href="#da">Datenerfassung und Verwaltung</a>
Alle während der Explorationsphase erkannten oder Berechneten Daten werden hier so abgespeichert, dass sie widerverwendet werden können. Als erstes wird die  Tag-Id von der Markerdetection gespeichert. Danach Ein Objekt Lamps, welches die erkannten Lampen enthaltet. Die letzten Daten, welche benötigt werden um eine Maschine zu verfollständigen sind die Koordinaten. Die zu speichernden Koordinaten werden vom Drive errechnet und auf den backwards befehl Übermittelt.  
Die erkannten Maschinen (MPS) werden alle über den Zentralen Broker gesendet um sie auf den anderen Robotinos auch zu speichern. Sobald die Map mit allen Maschinen komplettiert ist, wird sie retained an den zentralen Broker gesendet um die erkannten daten bei einem Neustart nicht zu verlieren. 

### <a href="#ab">Ablauf</a>
Zu beginn wird der Klasse das erste per String Ziel mitgeteilt. Die Klasse wandelt den String in ein Coord objekt um und wartet die Freigabe der Statemachine ab. Sobald die Freigabe eintrifft wird das Anfahren des entsprechenden Feldecken und das Feld wird nach einer MPS gescannt. Ist die MPS gefunden, wird diese angefahren und das Tag gescannt und an unsere Klasse gesendet. Für das erkennen der Lampe wird der Robotino noch näher an die MPS gefahren. Danach wird mit der oberen Kamera die aufleuchtenden Lampen gescannt und das erstellte Objekt an diese Klasse übermittelt. Vom Drive aus werden die Input und output Koordinaten berechnet und auch an uns gesendet. Auf den Befehl der Statemachine hin zum Rückwärtsfahren wird beim Zentralen Pc ein neues Feld angefordert. Der Zentrale Pc übermittelt eine neue Feldnummer als String. 
