[Home](home)  
[DokuSolidus](DokuSolidus)  

---------------------

## WayAnalyzer


## Drive
### Anpassung für Produktion

Damit die verschiedenen Positionen angefahren werden können haben wir beschlossen dass der ProduktioController der WayController mit dem "approach"
Befehl mitteilt welche Position angefahren werden muss. Dieser Befehl wird im WayController verarbeitet und als Übergabewert der Drive Klasse übergeben. In der approach Methode wird in einem Case die Offsetposition berechnet und danach als Ziel gesetzt. Danach wird diese, mit der setVeloCity Methode seitwärts angefahren. Als Abschluss wird die MPS mittels Infrarotsensor angefahren damit die Distanz möglichst genau ist.

### Parameter optimieren
  
Damit die Parameter überhaupt angepasst werden können müssen die Robotinos fahren damit wir verschiedene Einstellungen testen können. Wir haben die Werte so angepasst dass der Robotino sein Ziel schnell und genau anfahren kann. Die optimalen Werte wurden im Konfig File festgehalten.


## WayController  
  