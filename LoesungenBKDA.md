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
  
Der Robotino verfährt während dem Ausweichen seitwärts. Damit es keine Kollisionen geben kann, wurden die Methoden checkLeftSide() und checkRightSide() entwickelt. Die Methoden unterscheiden sich nur in den Richtungen welche sie überwachen. Während dem Ausweichen wird die entsprechende Methode aufgerufen. Diese vergleicht in einer breite von 30° die Laserwerte. sind mehr als fünf aufeinander folgende Laserwerte ungültig wird in die andere Richtung ausgewichen. Dies geschieht auf beide Seiten. Die Menge der aufeinander folgenden Laserwerte sind parametrierbar (Siehe tech. Wiki WayAnalyzer). 
  
### Zwischenraum Erkennung  
  
Der Robotino darf nicht versuchen durch eine zu schmale Schneise zu fahren und dann davor hin un her zu schwingen. Um dieses Problem zu lösen, wird ein Boolean gesetzt um sich zu Merken in welche Richtung bereits beschlossen wurde auszuweichen. So wird der Robotino vor einer zu kleinen Lücke nicht versuchen zwischendurch zu fahren und dann nicht beginnen zu schwingen. Dieser Boolean wird zurück gesetzt, sobald ein Hindernis direkt seitwärts detektiert wird oder er in die verbotene Zone vor der Bande fährt.
  
  
## Drive
### Anpassung für Produktion

Damit die verschiedenen Positionen angefahren werden können haben wir beschlossen dass der ProduktioController der WayController mit dem "approach"
Befehl mitteilt welche Position angefahren werden muss. Dieser Befehl wird im WayController verarbeitet und als Übergabewert der Drive Klasse übergeben. In der approach Methode wird in einem Case die Offsetposition berechnet und danach als Ziel gesetzt. Danach wird diese, mit der setVeloCity Methode seitwärts angefahren. Als Abschluss wird die MPS mittels Infrarotsensor angefahren damit die Distanz möglichst genau ist.

### Parameter optimieren
  
Damit die Parameter überhaupt angepasst werden können müssen die Robotinos fahren damit wir verschiedene Einstellungen testen können. Wir haben die Werte so angepasst dass der Robotino sein Ziel schnell und genau anfahren kann. Die optimalen Werte wurden im Konfig File festgehalten.


## WayController  
  
Damit auf die verschiedenen Positionen einer MPS gefahren werden kann, wurden im WayController die Case-Fälle erweitert. Je nachdem welche Meldung der ProductionController auf den Broker schreibt fällt das Case in einen anderen Aufgabenstatus. die Aufzurufende "approach"-Methode blieb gleich aber es muss eine andere Zahl als Übergabewert mitgegeben werden.  
Die Methode "approach" mit dem Übergabewert "0" wird in der Explorations- und in der Produktionsphase verwendet. Lediglich die Berechnungen unterscheiden sich. Dafür muss zusätzlich auf das Topic "phase" gehört werden. In der Explorationsphase werden nach "apprach(0)" die MPS Input- und Outputkoordinaten berechnet. Während der Produktion werden nach "apprach(0)" die Koordinaten des Robotinos neu gesetzt.