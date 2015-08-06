[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

### WayAnalyzer  

Der Wayanalyzer darf nicht nur einfachen Objekten ausweichen können, so wie er es bis Ende Prozessmodul getan hat. Er muss ihnen auch Ausweichen können, wenn die Objekte in komplexen Anordnungen zueinander stehen. 
Wenn der Robotino in unmittelbarer Nähe der Bande steht, darf er nicht gegen die Bande oder das Spielfeldende ausweichen. Da der Robotino seitwärts ausweicht und die Schneise immer in Fahrtrichtung verläuft, braucht es beim Ausweichen eine separate Möglichkeit die Seiten zu überwachen. Die Schneise ist für Seitwärtsbewegung zu klein um schnell genug ausweichen lassen zu können. Sollte der Robotino vor einer Schneise stehen, welche zu klein ist um durchfahren zu können, muss er begreifen dass er seitwärts weiterfahren muss.


  
### WayController  
  
#### Schlupf eleminieren
Damit der Schlupf, der beim Fahren entsteht, kompensiert werden kann, wird die Position nach jedem approach in der Produktionsphase auf den gespeicherten Wert zurückgesetzt. Da die gespeicherte Position einen halben Meter von der MPS entfernt ist muss die aktuelle Position des Robotinos berechnet werden bevor sie dem Positioncontroller übergeben wird.

#### Offsetpositionen anfahren
Die erhaltenen Nachrichten auf dem actions Topic enthalten die Informationen darüber welche Offsetposition der Robotino für die Produktion anfahren muss. Je nach Information wird ein anderer Übergabewert der approach Methode übergeben. Diese fährt danach an die gewünschte Position hin damit das Werkstück gegriffen werden kann. Nur die CS und RS haben zusätzliche Offsetpositionen auf der Input Seite die angefahren werden können.

  

### Drive

#### Anpassung für Produktion

Damit die Drive Klasse für die Produktion verwendet werden kann musste in der approach Methode einige Änderungen durchgeführt werden. Da sich der Robotino immer mit der Kamera am Tag orientiert ist es somit nicht möglich eine Offsetposition anzufahren. Damit dies möglich wird muss sich der Robotino in einem ersten Schritt am Tag ausrichten und danach seitwärts auf die gewünschte Position fahren. Sobald sich der Roboter am Tag ausgerichtet hat wird dem Drive ein neues Ziel gesetzt dass im nächsten Schritt seitwärts angefahren wird. Sobald diese erreicht wird fährt der Robotino langsam zur MPS hin.

#### Parameter optimieren

Damit die Parameter optimiert werden können müssen zahlreiche Tests durchgeführt werden. Während diesen Tests werden verschieden Parameter gewählt damit wir die optimale Werte finden können. Diese werden danach im Konfig File vermerkt damit diese für die nächsten Jahre erhalten bleiben.