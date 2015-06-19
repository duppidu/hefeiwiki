### Inhalt ###
- Allgemein
- Konstruktor
- messageArrived()
- jobHandler()
- saveMachine()


----------
### Allgemein ###

Diese Klasse handelt die Explorations-Phase des Spiels. Aufgerufen wird die Klasse von der State Machine.Die Klasse Stellt im Ablauf der Explorationphase ein zentrales Kommunikationsglied zwischen den Klassen Refbox, Waycontroller StateMachine, Marker-, LampDetection und den Anderen Robotinos dar. Zudem werden die Angefahrenen und erkannten MPS Daten gespeichert und Übermittelt. 

Ein Sequenz Diagramm finden sie  [Hier](ExploCommunication)
 
----------


### Konstruktor ###
Sobald die Klasse instantiiert wird, öffnet sie eine Kommunikation mit dem Mqtt-Brocker und hört auf die Topics auf denen Subscribed wurde (mqtt.setCallback( Reciever , Topic )).


----------


### messageArrived(String topic, MqttMessage message) ###
wird durch implements MqttCallback erzwungen

Diese Methode wird immer dann aufgerufen, wenn eine nachricht auf einem der Subscribten Topics publiziert wird. und die Methode erhält den Topic und die Nachricht als Übergabewert. Somit kann bei der nachricht auf das entsprechende Topic geprüft werden.  

----------

### jobHandler() ###

Beinhaltet 3x if Schleifen die dazue dienen, abzufragen welcher Robi aktiv ist.   
Je nachdem welcher Robi aktiv ist, werden dem Robi andere explorations Ziele zugeteilt. (Statisch einprogrammiert)    
Bei 6 zu explorierenden Maschinen sind je Robi 2 verschiedene Maschinen zugeteilt.   

Rükgabewert = [Coord](Coord) der zu explorierenden [Zone](Zones)   

----------

### saveMachine() ###

- Speichert eine neu detektierte [Maschine](Machine) mittels der Funktion [fill()](fill()).     
- Ermittelt [Maschinen](Machine) Informationen von der gegenüberliegenden Seite.   
- Speichert die Gegenüberliegende Seite der [Maschine](Machine) mit theoretische errechneten Werten ab.  

----------