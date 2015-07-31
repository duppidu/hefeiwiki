[Home](home)  
[DokuSolidus](DokuSolidus)  

---------------------

## WayAnalyzer  
### InfrarotSensor Ausweichmanöver  
  
Zuerst war die Infrarot-Distanzüberwachung in der CrashController-Klasse programmiert. Das neu mit den Infrarotsensoren auch ausgewichen werden muss, wurde das Ausweichen mit ihnen in der WayAnalyzer-Klasse programmiert.  
Folgende Bewegungen wurden programmiert, wenn mindestens ein Sensor einen ungültigen Wert aufweist:
- Die vorderen drei Sensoren lassen den Robotino rückwärts fahren.  
- Die linken zwei Sensoren lassen den Robotino nach rechts fahren.
- Die hinteren zwei Sensoren lassen den Robotino nach vorne fahren.
- Die rechten zwei Sensoren lassen den Robotino nach links fahren.
  
### Komplexe Objektanordnungen  
  
Durch die dynamisch Formel zu der Hindernis-Distanzüberwachung kann sich der Roboter bei Frontalen und seitens kombinierten Hindernissen rückwärts von den Objekten entfernen. Um dies zu realisieren wurde ebenfalls der Ausweichsmerker der Zwischenraumerkennung benötigt
  
### Hindernischeck während ausweichen   
  

  
### Zwischenraum Erkennung  
  

  
  
## Drive
### Anpassung für Produktion

Damit die verschiedenen Positionen angefahren werden können haben wir beschlossen dass der ProduktioController der WayController mit dem "approach"
Befehl mitteilt welche Position angefahren werden muss. Dieser Befehl wird im WayController verarbeitet und als Übergabewert der Drive Klasse übergeben. In der approach Methode wird in einem Case die Offsetposition berechnet und danach als Ziel gesetzt. Danach wird diese, mit der setVeloCity Methode seitwärts angefahren. Als Abschluss wird die MPS mittels Infrarotsensor angefahren damit die Distanz möglichst genau ist.

### Parameter optimieren
  
Damit die Parameter überhaupt angepasst werden können müssen die Robotinos fahren damit wir verschiedene Einstellungen testen können. Wir haben die Werte so angepasst dass der Robotino sein Ziel schnell und genau anfahren kann. Die optimalen Werte wurden im Konfig File festgehalten.


## WayController  
  
Da wir bis zum RoboCup leider nie in die Produktionsphase gekommen sind, sind die Programmierungen für die Produktionphase nie getestet worden. Theoretisch müssten die Ergänzungen für die Produktonsphase funktionieren. Der Code wurde zur Kontrolle mehrmals Schritt für Schritt gedanklich durchlaufen.