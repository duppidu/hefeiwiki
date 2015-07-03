[Home](home)   
[Back](DokuSolidus)    

----------

### Laserscanner

Der Code dazu wurde laufend getestet. Es gibt keinen festen Testplan. Ohne laufende Überprüfung der Funktion wäre das entwickeln schwierig gewesen.

**Stand letzter Test:**  
Der Laserscanner erkennt die richtige Maschine, wenn er im guten Winkel dazu steht. Er meldet zuverlässig, wenn er keine relevante Kante erkennt. Spätestens wenn der Robotino das dritte Mal aus einer anderen Ecke misst, erkennt er die Maschine.


### StateMachine

Die StateMachine wurde noch nicht in der Praxis getestet.

### Refbox
Die Kommunikation mit der Refbox wurde getestet. Grundsätzlich funktioniert sie. Momentan gibt es aber noch ein Problem mit der neusten Version der Refbox. 
Von den diversen Meldungen wurden bereits einige analysiert. Bei der ExplorationInfo und der OrderInfo gibt es bislang noch einige Unklarheiten über die empfangenen Nachrichten. Die sollten gelöst werden, sobald die neuste Version funktioniert.