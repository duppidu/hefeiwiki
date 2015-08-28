[Home](home)  
[Wiki](WikiSolidus)  

----------------------

# Änderungen und Ergänzungen Robocup
## Run
Da die Initialisierung der Roboter am Cup nicht so durchführbar war wie geplant, mussten wir die Initialisierung anpassen. Dies führte dazu, dass die Roboter direkt nebeneinander in der Einfahrt zum Spielfeld stehen. Damit die Robotinos während des Einfahrens nicht auf den Abstand der Banden reagieren, da sie sonst mit den anderen Robotinos kollidieren würden, wird im WayAnalyzer die avoidingDetector Methode erst aufgerufen, wenn der y Wert der aktuellen Position positiv ist. In der Einfahrtsschneise ist der y Wert negativ.

## SetAvoidspeed Methoden

Die Distanz zum Hindernis wurde zu Beginn statisch verglichen. Dies geschah mit Hilfe von parametrierbaren Distanzen.
Während der Diplomarbeit wurden die statischen Distanz-Vergleiche durch mathematische Formeln ersetzt. Dadurch ist es möglich je nach Geschwindigkeit und Distanz zum Hindernis mit variablen Geschwindigkeiten in X- und Y-Richtung auszuweichen. Die Ausweichsstärken können in den Config-Files nun angepasst werden

##CheckLeftSide und CheckRightSide
Diese Methoden wurden hinzugefügt um die linke und rechte Seite des Robotinos auf Hindernisse zu überprüfen. Sollte der Robotino rechts ausweichen wollen und sich ein Hindernis auf der rechten Seite befinden, wird die checkRightSide Methode ein True zurückgeben und somit weicht der Robotino auf die linke Seite aus. Um entscheiden zu können, ob sich ein Hindernis auf einer Seite befindet oder nicht, werden die Laserdaten mit einem parametrierbaren Wert verglichen. Sobald mehrere Werte kleiner sind, gibt die Methode ein True zurück.

## InfraredSensoring
Die Infrarotsensoren stoppen den Robotino nicht mehr. Im Gegenteil, wenn ein Wert eines Infrarotsensors die Sicherheitsdistanz unterschreitet, wird eine Geschwindigkeit gesetzt um die Distanz wieder zu vergrössern. Da dies jetzt eine Ausweichfunktion ist, befindet sich diese Methode nun im WayAnalyzer.

## MessageArrived
Da in der Formel zur Berechnung der Ausweichgeschwindigkeit die aktuelle Geschwindigkeit benötigt wird, muss diese zuerst von der messageArrived Methode empfangen werden. Die Nachricht wird in ein Speed Objekt gecastet und kann somit weiterverwendet werden.

## Run im WayController
Damit der Robotino während der Produktion zwischen den verschiedenen Positionen an der CS oder RS unterscheiden kann, wird der „approach“ Befehl mit einer Zahl über den Broker gegeben. Der Robotino berechnet danach die Position und fährt dort hin.
## CalcInOutCoord
Um abzuspeichern wo welche Maschine steht,  werden während der Explorationsphase die Input- und Output-Anfahrtspunkte berechnet, sobald der Robotino das Tag erkannt hat. Während den Inbetriebnahmen der Diplom-Arbeit wurde festgestellt, dass die trigonometrische Formel bei den Berechnungen von zwei Quadranten fehlerhaft war. Es wurde festgestellt, dass entsprechend mit einem falschen Winkel gearbeitet wurde. Die Formel wurde korrigiert und erfolgreich ausgetestet.
## CalcActCoord
Die Drehgeber verlieren je länger sie fahren die Genauigkeit. Um dieses Problem zu lösen, beschlossen wir die Koordinaten, welche abgespeichert wurden während der Explorationsphase um die Maschinen direkt anfahren zu können, zu verwenden. Wenn der Robotino nun während der Explorationsphase eine Maschine anfährt und sich dieser mit Hilfe des Lasers nähert, wird berechnet wo der Roboter in dem Moment, an dem er vor der Maschine steht, sein müsste. Entsprechend können die fehlerhaften Koordinaten der Drehgeber aufgefrischt werden. Das kann gelöst werden, indem sich der Roboter per Laser immer genau gleich vor die Maschine ausrichtet und stellt. Die Berechnungen dieser Methode sind ähnlich aufgebaut wie jene der CalcInOutCoord()-Methode.
