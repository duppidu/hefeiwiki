## Inhalt  

- Gedanken
- Materiell
- Ergebnis

## Gedanken 
  
### WayAnalyzer:  
  
Die WayController wurde bereits im Poe-Modul ausprogrammiert, ist aber noch nie getestet worden. Die Inbetriebnahme ist benötigt deshalb visuelle Feedbacks welche die Software an bestimmten Punkten zurück gibt. Der Überblick über den Testablauf muss beigehalten werden können, die Methoden müssen einzeln auf deren Funktion geprüft werden können.
  
### WayController:  
  
Es sollen die Input- und Outputkoordinaten der MPS berrechnet werden können. Diese Aufgabe muss mit Hilfe von Trigonometrie gelöst werden, das ds feld in X- und Y-Achsen unterteilt ist.
  
### CrashController:  
  
Sobald ein Crash geschieht soll der Roboter stoppen. Es soll falls möglich aber ein Crasch verhindert werden, oder diesen dem gegnirischen Team zugeschoben werden. Dazu braucht es eine Klasse welche versucht dies zu regeln.
  
## Materiell  
  
### WayAnalyzer:  
  
Um den Fahrablauf auszutesten wird ein Versuchsaufbau benötigt. Der Versuchsaufbau soll Ausweichssituationen simulieren, so wie diese am RoboCup ebenfalls auftreten werden. Die Ausweichedynamik soll im Solidus-Raum mit Hilfe der Versuchs-MPS und Kartonkisten ausgetestet werden.
  
### WayController:  
  
Es soll mit Hilfe von von Skizzen sämtlich Situationen skizziert werden wie die Maschine steht. Aus den Skizzen sollen die Positionsüberprüfungen übernommen werden können. Die Prüfbedingungen müssen die korrekten Formeln aufrufen können um an ein brauchbares Resultat zu gelangen. Die koordinaten sollen an die State-Machhine weitergeleitet werden können.
  
### CrashController:  
  
Um einen Crash zu verhindern oder diesen dem anderern Team zuzuschieben, sollen die Infrarot sensoren verwendet werden. Um weiteren Schaden während Kollisionen zu vermeiden wird der Bumper verwendet.
  
## Ergebnis  
  
### WayAnalyzer:  
  
Der Roboter soll die Zielkoordinaten erreichen ohne dabei ein Hindernis zu berühren. Die Hindernisse, müssen Umfahren werden können ohne das der Zielpunkt verloren geht. Der Einfluss der Fahrdynamik, soll per Broker an die Driveklasse weitergegeben werden.
  
### WayController:  
  
Sobald der Waycontroller von der State-Machine erfährt, ob das detektierte AR-Tag eine Input- oder Outputseite signalisiert, werden die Punkte berrechnet. 
Die punkte müssen berrechnet werden können da der Roboter die MPS-Station optimal Anfahren können muss, und er nicht auf optimaler Position steht wenn das Tag erkannt wird. Die Koordinaten sollen per Broker auf das entsprechende Topic gesendet werden können.
  
### CrashController:  
  
Wenn sich ein Objekt dem Roboter nähert sollen die Antriebe deaktiviert werden, dass der Roboter stehen bleibt um einen Crash zu verhindern oder den gegnerischen Roboter zu die Kollision herbeiführen zu lassen. Sobald eine Kollision geschehen sollte, soll der Roboter die Antriebe ebenfalls ausschalten. Dies massnahme ist um Schäden zu verhindern und um dem Wayanalyzer Zeit zu geben das Wegfahren zu Koordinieren.
  