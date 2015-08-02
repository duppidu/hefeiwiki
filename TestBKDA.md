[Home](home) [Back](DokuSolidus)  
  
## Inhalt
  
- Testkriterien und Auswertung
- HardwareTest
  
## Testkriterien und Auswertung  
  
Um die Funktionen während der Inbetriebnahme zu testen, wurde eine Checkliste erstellt. Diese enthält die Prüfkriterien.  
  
x = funktionstüchtig  
0 = Nicht geprüft  
f = funktioniert nicht, muss überarbeitet werden  
w = weggelassen

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
|Drive | approach 1 bis 4 | Die vier verschiedenen Offsetpositionen anfahren. | 0 |
|Drive | Parameter angepasst | Die Parameter so anpassen dass der Robotino schnell und genau sein Ziel erreicht.| x|
|WayAnalyzer| Dynamische Formel| Mit dynamischen Geschwindigkeiten ausweichen. |x|
|WayAnalyzer| Parameter angepasst | Parameter für die dynamische Formel anpassen.|x|
|WayAnalyzer| Ausweichen mit Infrarot| Die Infrarot halten immer einen Mindestabstand zu den Hindernissen.|x|
|WayAnalyzer| komplexe Hindernisanordnung| Aus komplexen Objektanordnungen hinaus oder hindurc manövrieren.|x|
|WayAnalyzer| Ausweiche Überwachung| Der Roboter erkennt während Seitwärtsbewegungen Hindernisse.|x|
|WayAnalyzer| Auf schmale Gänge reagieren| Der Roboter versucht nicht durch zu schmale Gänge zu fahren. Er umfährt solche.|x|
|WayController| Anpassungen Produktion| Der WayController mit den verschiedenen Anfahrmöglichkeiten testen.| 0|
|WayController| Anfahrtspunkte berechnen| Korrektur der Berechnungen der Anfahrtspunkte.| x|

 


## Prüfverfahren WayAnalyzer

Das Prüfverfahren lief gleich wie im Prozessmodul, dass bedeutet der Robotino musste durch einen Hindernisparcours fahren ohne dass er einen Crash verursacht. Dabei wurden die Parameter der Formel verändert und die optimalen Werte im Kofig Flie festgehalten.
Es wurde getestet:  
- Es wurden mehrere Objekt sehr Nahe aneinander in verschiedenen Winkel aufgestellt. So musste er die Seiten während dem Ausweichen überprüfen, durfte nicht vor einer zu schmalen Schneise hängen bleiben, nicht in ungültige Zonen fahren und er musste es an das Tiel schaffen.
- Es wurde überprüft ob der Roboter mit Hilfe der Infrarotsensoren richtig auswich. Indem man ihm schnell und Nahe genug ein Hindernis in die Fahrbahn stellte.
-

## Prüfverfahren WayController  

Die Berechnungen für die Anfahrtspunkt welche im PM-Kurs programmiert wurden, waren leider Fehlerhaft. Entsprechend wurden die Trigonometrischen Fehler gefunden und behoben. Dies geschah mit Hilfe des Brokers und den Loglisten. Die Berechneten Koordinaten wurden nachgerechnet. Anschliessend wurden die Formeln nochmals Überprüft und den Fehler in der Trigonometrischen Formel behoben. 
  
Da wir bis zum RoboCup leider nie in die Produktionsphase gekommen sind, sind die Programmierungen für die Produktionphase nie getestet worden. Theoretisch müssten die Ergänzungen für die Produktonsphase funktionieren. Der Code wurde zur Kontrolle mehrmals Schritt für Schritt gedanklich durchlaufen.  
  
## Prüfverfahren Drive

Die "approach"-Methode konnte nicht getestet werden da die Zeit nicht gereicht hat. Am Robocup wurde die gesamte Zeit in die Exploration gesteckt. Aus diesem Grund konnte keine Zeile der Produktionsphase getestet werden.
  