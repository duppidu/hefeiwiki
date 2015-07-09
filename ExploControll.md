[Home](home) [Back](WikiSolidus)

### Inhalt ###
- Allgemein
- Konstruktor
- messageArrived()
- jobHandler()
- saveMachine()
- handleexploCoords()


----------
### Allgemein ###

Diese Klasse handelt die Explorations-Phase des Spiels.  
Aufgerufen wird die Klasse von der State Machine.  
Die Klasse Stellt im Ablauf der Explorationphase ein zentrales Kommunikationsglied zwischen den Klassen Refbox,  
Waycontroller StateMachine, Marker-, LampDetection und den Anderen Robotinos dar.
Es werden fix einprogrammierte Ziele an die entsprechenden Robis gesendet,  
damit wird die Suche der MPS beschleunigt und verhindert,  
dass zwei Robis am selbern Ort suchen.    
Zudem werden die Angefahrenen und erkannten MPS Daten gespeichert und Übermittelt. 

Ein Sequenz Diagramm finden sie  [Hier](ExploCommunication)
 
----------


### Konstruktor ###
Sobald die Klasse instantiiert wird, öffnet sie eine Kommunikation mit dem Mqtt-Brocker und hört auf die Topics auf denen Subscribed wurde (mqtt.setCallback( Reciever , Topic )).


----------


### messageArrived() ###
wird durch implements MqttCallback erzwungen

Diese Methode wird immer dann aufgerufen, wenn eine nachricht auf einem der Subscribten Topics publiziert wird. und die Methode erhält den Topic und die Nachricht als Übergabewert. Somit kann bei der nachricht auf das entsprechende Topic geprüft werden.  



----------

### jobHandler() ###

- Beinhaltet 3x if Schleifen die dazue dienen, abzufragen welcher Robi aktiv ist.   
- Je nachdem welcher Robi aktiv ist, werden dem Robi andere explorations Ziele([Zonen](Zones)) zugeteilt. (Statisch einprogrammiert)    
- Bei 6 zu explorierenden Maschinen sind je Robi 2 verschiedene [MPS](Machine) zugeteilt.  
- Die [Koordinaten](Coord) der zu explorierenden [Zone](Zones) kommt aus der ArrayList `coord` aus [Zones()](Zones).  

Rükgabewert = [Coord](Coord) der zu explorierenden [Zone](Zones)   

----------

### saveMachine() ###

- Speichert eine neu detektierte [Maschine](Machine) mittels der Funktion [fill()](Machine).     
- Ermittelt [MPS](Machine) Informationen von der gegenüberliegenden Seite.   
- Speichert die Gegenüberliegende Seite der [MPS](Machine) mit theoretische errechneten Werten mittels der Funktion [fill()](Machine).   
- Überprüft beim Speichern einer neuen [MPS](Machine) ob es wirklich eine neue [MPS](Machine) ist!

----------
### handleexploCoords() ###


Übergabewert = String[] von ..


----------