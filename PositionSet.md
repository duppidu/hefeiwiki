[Back](wikisolidus)  
[Home](home)  
***
## PositionSet
Um die Position bei StartUp zu setzen, wird die Methode initPos() in der Klasse Drive() aufgerufen.
### Aktuelles Vorgehen
Um die Position am Anfang zu setzen, werden die Robotinos genau auf vorher am Boden markierte Stellen gesetzt und ausgerichtet.
Ganz am Anfang der Explorationsphase werden die Punkte als aktuelle Position gesetzt. Da die Punkte vorher genau ausgemessen wurden und so bekannt sind, können sie nur noch fest im Code eingegeben werden.  
**Vorgehen:**  
1. Vor Spielbeginn müssen drei feste Punkte ausgemessen und am Boden markiert werden, an welchen die Robotinos starten. (Die ausgemessenen Punkte müssen am Nullpunkt des Feldes gespiegelt sein.)

2. Die Koordinaten der Punkte von der **Seite Cyan** müssen in der Klasse [Drive](Drive) im Konstruktor in das Array startCoords eingegeben werden. Beim Start auf der Magentaseite werden die Koordinaten automatisch angepasst.

3. Die Robotinos müssen genau auf die 3 Punkte gestellt werden. Sobald die Explorationsphase startet fahren sie los.

![Unbenannt](https://gitlab.com/solidus/hefei/uploads/7ec1033a7c79b865539fcfd3e7ae6f63/Unbenannt.png)

**Achtung:** Die oben beschriebene Methode ist eine kurzfristig programmierte (am Robocup 2015) Möglichkeit. Ursprünglich war folgende Methode vorgesehen. Diese funktionierte zuverlässiger, darf aber so momentan nicht gebraucht werden.  
Siehe auch: [Verbesserung der Positionierung](PositionSetVerbesserung)
### Ursprüngliches Vorgehen
Die Robotinos setzen ihre aktuelle Position nacheinander in der Setupphase und fahren danach auf vordefinierte Punkte auf das Feld. Sobald der vordere seine Position mithilfe des Lasers und den bekannten Entfernungen der Banden gesetzt hat und den Startbereich verlassen hat, kommt der nächste nach und tut dasselbe.

**Vorgehen:**
1. Vor Spielbeginn müssen die Positionen der unteren und die Seitenbande ausgemessen und Drive.xml File abgespeichert werden.
2. Der Robotino muss in der Einfahrt zum Feld stehen und Richtung Koordinatennullpunkt schauen. Der Robotino muss einigermassen gerade stehen. (Die Reihenfolge der Robotinos muss stimmen)

3. Der Robotino fährt automatisch auf eine zuvor definierte Distanz auf die Bande vor sich zu.

4. Der Laser misst die Entfernung von der Bande vor sich und je nach Teamfarbe die rechte oder die linke Bande und setzt so aus den bekannten Distanzwerten der Banden seine Anfangsposition.


![StartUp](https://gitlab.com/solidus/hefei/uploads/63d0861e0e6938c947947a417e7165bf/StartUp.JPG)
