[Home](home) [Back](DokuSolidus)  
  
## Inhalt
  
- Testkriterien und Auswertung
- HardwareTest
  
## Testkriterien und Auswertung  
  
Um die Funktionen während der Inbetriebnahme wurde eine Checkliste erstellt. Diese enthält die Prüfkriterien.  
  
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
|WayController| Anpassungen Produktion| Der WayController mit den verschiedenen Anfahrmöglichkeiten testen.| 0|
|WayAnalyzer| Ausweichen mit Infrarot| Die Infrarot halten immer einen Mindestabstand zu den Hindernissen.|x|
 


## Prüfverfahren WayAnalyzer

Das Prüfverfahren lief gleich wie im Prozessmodul, dass bedeutet der Robotino musste durch einen Hindernisparcours fahren ohne dass er einen Crash verursacht. Dabei wurden die Parameter der Formel verändert und die optimalen Werte im Kofig Flie festgehalten.

## Prüfverfahren WayController

## Prüfverfahren Drive

Die approach Methode konnte nicht getestet werden da die Zeit nicht gereicht hat. Am Robocup wurde die gesamte Zeit in die Exploration gesteckt. Aus diesem Grund konnte keine Zeile der Produktionsphase getestet werden.
  