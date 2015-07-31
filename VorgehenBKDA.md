[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

### WayAnalyzer  


  
### WayController  
  
Damit die Produktion funktionieren kann, muss die Driveklasse korrekt angesteuert werden. Dazu muss der Waycontroller erweitert werden. In der Exploration werden die Input- und Output-Anfahrtspunkte berechnet. Nun müssen für die Produktion auch die Koordinaten neu gesetzt werden. Jedes mal wenn in der Produktion ein "approach" (das Annähern zu einer MPS) durchgeführt wird, werden die Koordinaten neu gesetzt. So kann die Positionsgenauigkeit aufrecht erhalten werden.  
Des weiteren, besitzen die "MPS" diverse Anfahrpositionen.
- Die Cap-Station besitzt nebst dem Band drei weitere Anfahrtspositionen.
- Die Ringstation besitzt nebst dem Band eine weitere Anfahrtsposition.
Der Robotino fährt zuerst auf die Position vor der Maschine, als nächstes wird ein "approach.2" empfangen. Dann fährt der Robotino entsprechend nicht zum Band, sondern zu dem versetzten Liegeplatz. Anschliessend soll das dort stationierte Teil gegriffen und rückwärts gefahren werden.
  

### Drive

#### Anpassung für Produktion

Damit die Drive Klasse für die Produktion verwendet werden kann musste in der approach Methode einige Änderungen durchgeführt werden. Da sich der Robotino immer mit der Kamera am Tag orientiert ist es somit nicht möglich eine Offsetposition anzufahren. Damit dies möglich wird muss sich der Robotino in einem ersten Schritt am Tag ausrichten und danach seitwärts auf die gewünschte Position fahren. Sobald sich der Roboter am Tag ausgerichtet hat wird dem Drive ein neues Ziel gesetzt dass im nächsten Schritt seitwärts angefahren wird. Sobald diese erreicht wird fährt der Robotino langsam zur MPS hin.

#### Parameter optimieren

Damit die Parameter optimiert werden können müssen zahlreiche Tests durchgeführt werden. Während diesen Tests werden verschieden Parameter gewählt damit wir die optimale Werte finden können. Diese werden danach im Konfig File vermerkt damit diese für die nächsten Jahre erhalten bleiben.