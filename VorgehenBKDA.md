[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

### WayAnalyzer  


  
### WayController  
  

  

### Drive

Damit die Drive Klasse für die Produktion verwendet werden kann musste in der approach Methode einige Änderungen durchgeführt werden. Da sich der Robotino immer mit der Kamera am Tag orientiert ist es somit nicht möglich eine Offsetposition anzufahren. Damit dies möglich wird muss sich der Robotino in einem ersten Schritt am Tag ausrichten und danach seitwärts auf die gewünschte Position fahren. Sobald sich der Roboter am Tag ausgerichtet hat wird dem Drive ein neues Ziel gesetzt dass im nächsten Schritt seitwärts angefahren wird. Sobald diese erreicht wird fährt der Robotino langsam zur MPS hin.