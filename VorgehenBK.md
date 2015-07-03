[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

### WayAnalyzer  
  
Der WayAnalyzer war bereits aus programmiert. Bevor wir ihn in Betrieb genommen haben, haben wir den den Code nochmals auf Fehler überprüft. Anschliessend haben wir  auf der Teststrecke den Roboter in Betrieb genommen. Die Abnahme des Roboters mit Hilfe der Checkliste ist auf dem Artikel [Test](TestBK) zu finden. Obwohl die Grundidee das Ausweichen zu realisieren gut durchdacht war, gab es viele Ergänzungen und Anpassungen zu machen. Während dem ersten Verfahrversuch, stellten wir fest, dass die CPU Auslastung auf 120% lag. Der Fehler beim einlesen des Laserarrays. Das Array war auf 271 Position begrenzt, dies führte zu einem Fehler.  
Des weiteren, waren die Schneisenberechnungen nicht optimiert. Resultate, welche mehrfach verwendet wurden, sind immer wieder neu berechnet worden. Diese wurde für die komplette Klasse angepasst um die CPU-Auslastung zu minimieren.  
Während späteren Testfahrten wurde festgestellt, dass die Ausweichsprioritäten-Regelung nicht funktionierte. Der Roboter erkannte ein Hindernis auf der linken Seite und als er dann nach rechts zog, erkannte er sogleich die Wand und steuerte wieder auf auf das linke Hindernis zu.  
Zwischenzeitlich hatten wir das Problem, dass der Laser falsche Werte zurückgab. Wir können nicht überprüfen wie korrekt die Distanzwerte sind welche wir erhalten. Wir können nur die Distanzen welche den Wert 0.0 aufweisen als ungültig erklären. Das Problem war das während der Inbetriebnahme die 0.0 Werte auch als Hindernisdistanz ausgewertet worden sind.

  
### WayController  calcInOutCoord()  
  
Durch die von mir angefertigten Skizzen, welche für sämtliche Position auf denen die Maschinen stehen können die Passende Formel enthält, war die Programmierung der Methode schnell ausprogrammiert. Zuerst war geplant die Methode aufzurufen, sobald der Roboter an der Input-Seite der Maschine steht. Später wurde fest gestellt, das mit dem funktionierenden WayAnalyzer nicht mehr nötig sein wird, zuerst auf die Input-Seite zu fahren. Die Methode calcInOutCoord() muss nun von beiden Seiten die Input und Outputkoordinaten zu berechnen. Die Methode musste erweitert werden mit dem aktuellen Standort vor der MPS an welcher der Roboter steht. Das heisst, der WayController empfängt zusätzlich per Broker ob der Roboter auf einer Input oder Outputseite steht. Die Berechnungen um die Koordinaten zu erhalten, mussten nicht angepasst werden, lediglich wann auf welches Topic gesendet werden muss.  
Durch unseren aktuellen Fortschritt war es uns nicht möglich die Methode zu testen. Dies wird ein Bestandteil der Diplomarbeit werden.
  
### CrashController  
  
Um den Bumper und die Infrarotsensoren auszuwerten, setzte ich mich mit der Api2-doc auseinander. Diese ist leider nicht sehr gut beschrieben. Das führte dazu, dass ich ausprobierte welche Methode die von mir gewünschten Funktionen ausführt.

### Drive

Die Drive Klasse funktionierte zu Beginn des Prozessmodules schon. Die Aufgabe war jedoch diese Klasse zu optimieren und eine Kommunikation mit dem WayAnalyzer herzustellen.  
Damit das Programm kleiner wird haben wir beschlossen den gesamten Code noch einmal durch zu gehen. Als wir auf die Methoden machineAlign und targetAlign gestossen sind, haben wir beschlossen diese zusammenzuführen. Damit dies realisiert werden kann musste ein Übergabewert hinzugefügt werden. Dieser Übergabewert beinhaltet den Winkel der erreicht werden muss damit ein "true" zurück kommt. Das bedeutet dass beim Aufruf entweder der Winkel berechnet werden muss oder einfach das target mitgegeben wird.  
Damit der Robotino ausweichen kann muss die Kommunikation zwischen Drive und WayAnalyzer erstellt werden. Diese Aufgabe konnte einfach mit dem Broker erledigt werden. Der WayAnalyzer sendet bei einer sich ändernden Geschwindigkeit eine Nachricht auf ein Topic. Die Drive Klasse berücksichtigt dieses Topic und wandelt danach die Geschwindigkeiten korrekt um, damit diese an das Omnidrive weitergegeben werden können. Damit die Geschwindigkeiten problemlos übertragen werden können wurde die Speed Klasse verwendet. Diese beinhaltet drei Float Werte die für X, Y und Omega stehen. 