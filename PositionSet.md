[Back](wikisolidus)
## PositionSet

Um die Position am Anfang zu setzen, werden die Robotinos genau auf vorher am Boden markierte Stellen gesetzt und ausgerichtet.
Ganz am Anfang der Explorationsphase werden die Punkte als aktuelle Position gesetzt. Da die Punkte vorher genau ausgemessen wurden und so bekannt sind, können sie nur noch fest im Code eingegeben werden.  
**Vorgehen:**  
1. Vor Spielbeginn müssen drei feste Punkte ausgemessen und am Boden markiert werden, an welchen die Robotinos starten. (Die ausgemessenen Punkte müssen am Nullpunkt des Feldes gespiegelt sein.)

2. Die Koordinaten der Punkte müssen in der Klasse [Drive](Drive) im Konstruktor in das Array startCoords eingegeben werden.

3. 

**Achtung:** Die oben beschriebene Methode ist eine kurzfristig programmierte (am Robocup 2015) Möglichkeit. Ursprünglich war folgende Methode vorgesehen. Diese funktionierte zuverlässiger. 

Um die Position bei StartUp zu setzen, wird die Methode initPos() in der Klasse Drive() aufgerufen.

1. Der Robotino muss in der Einfahrt zum Feld stehen und Richtung Koordinatennullpunkt schauen. Der Robotino muss einigermassen gerade stehen.

2. Der Robotino fährt automatisch auf eine zuvor definierte Distanz auf die Bande vor sich zu.

3. Der Laser misst die Entfernung von der Bande vor sich und je nach Teamfarbe die rechte oder die linke Bande und setzt so aus den bekannten Distanzwerten der Banden seine Anfangsposition.


![StartUp](https://gitlab.com/solidus/hefei/uploads/63d0861e0e6938c947947a417e7165bf/StartUp.JPG)
