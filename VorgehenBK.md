[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

### WayAnalyzer  
  
Der WayAnalyzer war bereits ausprogrammiert. Bevor wir ihn in Betrieb genommen haben, haben wir den den Code nochmals auf Fehler überprüft. Anschliessend haben wir  auf der Teststrecke den Roboter in Betrieb genommen. Die Abnahme des Roboters mit Hilfe der Checkliste ist auf dem Artikel [Test](TestBK) zu finden. Obwohl die Grundidee das Ausweichen zu realisieren gut durchdacht war, gab es viele Ergänzungen und Anpassungen zu machen. Während dem ersten Verfahrersuch, stellten wir fest, dass die CPU Auslastung auf 120% lag. Der Fehler beim einlesen des Laserarrays. Das Array war auf 271 Position begrenzt, dies führte zu einem Fehler.  
Des weiteren, waren die Schneisenberechnungen nicht optimiert. Resultate, welche mehrfach verwendet wurden, sind immer wieder neu berechnet worden. Diese wurde für die komplette Klasse angepasst um die CPU-Auslastung zu minimieren.  
Während späteren Testfahrten wurde festgestellt, dass die Ausweichsprioritäten-Regelung nicht funktionierte. Der Roboter erkannte ein Hindernis auf der linken Seite und als er dann nach rechts zog, erkannte er sogleich die Wand und steuerte wieder auf auf das linke Hindernis zu.  
Zwischenzeitlich hatten wir das Problem, dass der Laser falsche Werte zurückgab. Wir können nicht überprüfen wie korrekt die Distanzwerte sind welche wir erhalten. Wir können nur die Distanzen welche den Wert 0.0 aufweisen als ungültig erklären. Das Problem war das während der Inbetriebnahme die 0.0 Werte auch als Hindernisdistanz ausgewertet worden sind.

  
### WayController  calcInOutCoord()  
  
Durch die von mir angefertigten Skizzen, welche für sämtliche Position auf denen die Maschinen stehen können 
  
### CrashController  
  

  