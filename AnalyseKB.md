[Home](home)  
[DokuSolidus](DokuSolidus)  
[Konzept](KonzeptBK)  
----------

## Inhalt  

- Gedanken
- Materiell
- Ergebnis

## Gedanken 
  
### WayAnalyzer:  
  
Die WayController wurde bereits im Poe-Modul ausprogrammiert, ist aber nicht getestet worden. Die Inbetriebnahme ist deshalb nötig um visuelle Feedbacks, welche die Software an bestimmten Punkten zurück gibt, zu erhalten. Der Überblick über den Testablauf muss beibehalten werden können, die Methoden müssen einzeln auf deren Funktion geprüft werden können.
  
### WayController:  
  
Es sollen die Input- und Outputkoordinaten der MPS berechnet werden können. Diese Aufgabe muss mit Hilfe von Trigonometrie gelöst werden, da das Feld in X- und Y-Achsen unterteilt ist.
  
### CrashController:  
  
Sobald ein Crash geschieht soll der Roboter stoppen. Es soll falls möglich aber ein Crash verhindert werden, oder diesen dem gegnerischen Team zugeschoben werden. Dazu braucht es eine Klasse welche versucht dies zu regeln.

### Drive

Da diese Klasse schon im Poe erstellt und getestet wurde, muss sie im Prozessmodul noch optimiert werden. Diese Aufgabe beinhaltet die Kommunikation zwischen WayAnalyzer und Drive zu verbessern sowie einige Methoden zu optimieren.
  
## Materiell  
  
### WayAnalyzer:  
  
Um den Fahrablauf auszutesten wird ein Versuchsaufbau benötigt. Der Versuchsaufbau soll Ausweichsituationen simulieren, so wie diese am RoboCup ebenfalls auftreten werden. Die Ausweichedynamik soll im Solidus-Raum mit Hilfe der Versuchs-MPS und Kartonkisten ausgetestet werden.
  
### WayController:  
  
Es soll mit Hilfe von Skizzen sämtlich Situationen skizziert werden wie die Maschine steht. Aus den Skizzen sollen die Positionsüberprüfungen übernommen werden können. Die Prüfbedingungen müssen die korrekten Formeln aufrufen können um an ein brauchbares Resultat zu ergeben. Die Koordinaten sollen an die State-Machhine weitergeleitet werden können.
  
### CrashController:  
  
Um einen Crash zu verhindern, sollen die Infrarot Sensoren verwendet werden. Um weiteren Schaden während Kollisionen zu vermeiden wird der Bumper verwendet.

### Drive

Damit die Methoden des Drives verbessert werden können müssen alle möglichen Situation, wie zum Beispiel einen Stopp, getestet werden. Um die Methode zu optimieren wird der gesamte Code erneut durchgelesen um unnötige Berechnungen zu löschen. Die Kommunikation zwischen den beiden Klassen Drive und WayAnalyzer wird benötigt um ausweichen zu können. Diese soll ausschliesslich über den Broker gehen.
  
## Ergebnis  
  
### WayAnalyzer:  
  
Der Roboter soll die Zielkoordinaten erreichen ohne dabei ein Hindernis zu berühren. Die Hindernisse, müssen Umfahren werden können ohne das der Zielpunkt verloren geht. Der Einfluss der Fahrdynamik, soll per Broker an die Drive Klasse weitergegeben werden.
  
### WayController:  
  
Sobald der Waycontroller von der State-Machine erfährt, ob das detektierte AR-Tag eine Input- oder Outputseite signalisiert, werden die Punkte berechnet. 
Die punkte müssen berechnet werden können da der Roboter die MPS-Station optimal Anfahren können muss, und er nicht auf optimaler Position steht wenn das Tag erkannt wird. Die Koordinaten sollen per Broker auf das entsprechende Topic gesendet werden können.
  
### CrashController:  
  
Wenn sich ein Objekt dem Roboter nähert sollen die Antriebe deaktiviert werden, dass der Roboter stehen bleibt um einen Crash zu verhindern oder den gegnerischen Roboter zu die Kollision herbeiführen zu lassen. Sobald eine Kollision geschehen sollte, soll der Roboter die Antriebe ebenfalls ausschalten. Dies Massnahme ist um Schäden zu verhindern und um dem Wayanalyzer Zeit zu geben das Wegfahren zu Koordinieren.

### Drive

Durch Absprache mit dem Team wurde bei der goToTarget Methode die machineAlign Methode hinzugefügt damit diese automatisch durch das Drive aufgerufen wird. Die machineAlign und targetAlign Methode wurden zur Align Methode zusammengeführt. Der Grund dafür ist dass diese Methoden sehr ähnlich sind und durch wenige Änderungen zusammengeführt werden können. Die Kommunikation zwischen WayAnalyzer und Drive wurde mittels Speed Klasse realisiert. Diese wird vom WayAnalyzer geschrieben und dann über den Broker gesendet. Das Drive empfängt diese Klasse dann und überschreibt danach die eigenen Geschwindigkeiten.
  