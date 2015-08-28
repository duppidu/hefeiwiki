[Home](home)  
[DokuSolidus](DokuSolidus)  

---------------------

# Lösungen
## WayAnalyzer
### Infrarotsensor Ausweichmanöver

Ursprünglich war die Infrarot-Distanzüberwachung in der CrashController-Klasse programmiert. Da jetzt die Distanz der Infrarotsensoren genutzt wird um Hindernissen auszuweichen, wurde diese Funktion in die WayAnalyzer-Klasse versetzt.
Folgende Bewegungen wurden programmiert, wenn mindestens ein Sensor einen ungültigen Wert aufweist:

- Die vorderen drei Sensoren lassen den Robotino rückwärts fahren.
- Die linken zwei Sensoren lassen den Robotino nach rechts fahren.
- Die hinteren zwei Sensoren lassen den Robotino nach vorne fahren.
- Die rechten zwei Sensoren lassen den Robotino nach links fahren.

### Zwischenraum Erkennung

Der Robotino darf nicht versuchen durch eine zu schmale Schneise zu fahren und anschliessend davor hin und her schwingen. Um dieses Problem zu lösen, wird ein Boolean (Ausweichsmerker) gesetzt um sich zu merken, in welche Richtung bereits ausgewichen wurde. So wird der Robotino vor einer zu schmalen Lücke nicht versuchen zwischendurch sondern um das Objekt herum zu fahren. Dieser Merker wird erst zurückgesetzt, wenn sich kein Hindernis mehr im Weg befindet oder auf die andere Seite ausgewichen wird.

### Komplexe Objektanordnungen

Durch die dynamische Formel zur Berechnung der Ausweichgeschwindigkeit und der Einsatz des Ausweichsmerkers kann sich der Roboter bei frontalen und seitwärts anliegenden Hindernissen rückwärts von den Objekten entfernen und somit jegliche Hindernisanordnung umgehen.

### Hindernischeck während dem Ausweichen

Der Robotino fährt während dem Ausweichen seitwärts. Damit es keine Kollisionen geben kann, wurden die Methoden checkLeftSide() und checkRightSide() entwickelt. Die Methoden unterscheiden sich nur in den Richtungen, welche sie überwachen. Diese Methoden werden während dem Entscheid, in welche Richtung er ausweichen wird, aufgerufen. Diese vergleichen in einer Breite von 30° die Laserwerte. Sind mehr als fünf aufeinander folgende Laserwerte kleiner als der eingestellte Wert, wird „True“ zurückgegeben. Die Menge der aufeinander folgenden Laserwerte sind parametrierbar (Siehe tech. Wiki WayAnalyzer). 


## Drive

### Anpassung für Produktion

Damit die verschiedenen Positionen der diversen MPS-Stationen angefahren werden können, haben wir beschlossen, dass der ProduktionController dem WayController mit dem "approach" Befehl mitteilt, welche Position angefahren werden muss. Dieser Befehl wird im WayController verarbeitet und als Übergabewert der Drive Klasse übergeben. In der approach() Methode wird in einem Case die Offsetposition berechnet und danach als Ziel gesetzt. Danach wird diese mit der setVeloCity() Methode seitwärts angefahren. Als Abschluss wird die MPS mittels Infrarotsensor angefahren, damit die Distanz möglichst genau ist.

### Parameter optimieren

Bevor die Parameter überhaupt optimiert werden können, mussten die Robotinos mit verschiedenen Parametereinstellungen fahren, um die optimalen Parameter zu finden. Wir haben die Werte so angepasst, dass der Robotino sein Ziel schnell und genau anfahren kann. Die optimalen Werte wurden im Config-File festgehalten.

## WayController

Damit auf die verschiedenen Positionen einer MPS gefahren werden kann, wurden im WayController die Case-Fälle erweitert. Je nachdem, welche Meldung der ProductionController auf den Broker schreibt, fällt das Case in einen anderen Aufgabenstatus. Die aufzurufende approach() Methode blieb gleich, aber es muss neu eine Zahl als Übergabewert mitgegeben werden.
Die approach() Methode mit dem Übergabewert "0" wird in der Explorations- und Produktionsphase verwendet. Lediglich die Berechnungen für Produktion und Exploration unterscheiden sich. Dafür muss zusätzlich auf das „phase“ Topic gehört werden. In der Explorationsphase werden nach approach(0) die MPS Input- und Outputkoordinaten berechnet. Während der Produktion werden nach approach(0) die Koordinaten des Robotinos neu gesetzt, um die Drehgeberabweichung zu korrigieren.
