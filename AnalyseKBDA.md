[Home](home)  
[DokuSolidus](DokuSolidus)  
[Konzept](KonzeptBKDA)  

----------

## Inhalt  

- Gedanken
- Materiell
- Ergebnis

## Gedanken 
  
### WayAnalyzer:  
  
Die Formel die die Geschwindigkeiten berechnet muss gut durchdacht werden, damit diese schnell getestet werden kann. Auch einzelne Spezialfälle müssen behandelt werden können, zum Beispiel der Robotino soll beim Ausweichen das Spielfeld nicht verlassen. Diese Spezialfälle müssen einzeln getestet werden.
  
### WayController:  
  
Ken bitte usfülle
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
Es sollen die Input- und Outputkoordinaten der MPS berechnet werden können. Diese Aufgabe muss mit Hilfe von Trigonometrie gelöst werden, da das Feld in X- und Y-Achsen unterteilt ist.

### Drive

Um die zusätzlichen Positionen an den Capstations und Ringstations anfahren zu können müssen wir mit dem Produktionsteam eine Methode finden wie sie und dieses mitteilen. Danach können wir diese Methode anpassen und testen.
  
## Materiell  
  
### WayAnalyzer:  
  
Um den Fahrablauf auszutesten wird ein Versuchsaufbau benötigt. Der Versuchsaufbau soll Ausweichsituationen simulieren, so wie diese am RoboCup ebenfalls auftreten werden. Die Ausweichedynamik soll im Solidus-Raum mit Hilfe der Versuchs-MPS und Kartonkisten ausgetestet werden.
  
### WayController:  

Ken bitte usfülle
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
Es soll mit Hilfe von Skizzen sämtlich Situationen skizziert werden wie die Maschine steht. Aus den Skizzen sollen die Positionsüberprüfungen übernommen werden können. Die Prüfbedingungen müssen die korrekten Formeln aufrufen können um an ein brauchbares Resultat zu ergeben. Die Koordinaten sollen an die State-Machhine weitergeleitet werden können.

### Drive

Damit wir diese Methode testen können muss das Programm den entsprechenden Befehl über den Broker erhalten. Danach können die Parameter überprüft und wenn nötig korrigiert werden.
  
## Ergebnis  
  
### WayAnalyzer:  
  
Der Roboter soll die Zielkoordinaten erreichen ohne dabei ein Hindernis zu berühren. Die Hindernisse, müssen Umfahren werden können ohne das der Zielpunkt verloren geht. Der Einfluss der Fahrdynamik, soll per Broker an die Drive Klasse weitergegeben werden.
  
### WayController:  
 
Ken bitte usfülle
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
Sobald der Waycontroller von der State-Machine erfährt, ob das detektierte AR-Tag eine Input- oder Outputseite signalisiert, werden die Punkte berechnet. 
Die punkte müssen berechnet werden können da der Roboter die MPS-Station optimal Anfahren können muss, und er nicht auf optimaler Position steht wenn das Tag erkannt wird. Die Koordinaten sollen per Broker auf das entsprechende Topic gesendet werden können.
  

### Drive

Das Drive sollte während der Produktionsphase die Positionen ohne Problem anfahren können.

  