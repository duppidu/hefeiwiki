[Home](home) [Back](DokuSolidus)  
  
## Inhalt
  
- Testkriterien und Auswertung
- HardwareTest
  
## Testkriterien und Auswertung  
  
Um die Funktionen während der Inbetriebnahme wurde eine Checkliste erstellt. Diese enthält die Prüfriterien.  
  
x = funktionstüchtig  
0 = Nicht geprüft  
f = funktioniert nicht, muss überarbeitet werden  
w = weggelassen

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| WayAnalyzer|LaserArray|Wird das LaserArray mit korrekten Werten gefüllt und aktualisiert |X |
| WayAnalyzer|avoidingDetector()|Die Zählung der ugültgen Werte muss gelöscht werden sobald ein Laserwert dazwischen gültig ist. So werden falsche Messungen annuliert|X |
| WayAnalyzer|avoidingDetector()|Die Winkel der Laserpositionen müssen korrekt bstimmt werden|X |
| WayAnalyzer|avoidingDetector()|Die kleinste ungültige Distanz muss in jedem Zyklus gespeichert werden|X |
| WayAnalyzer|avoidingDetector()|Es muss die korekte Ausweich-Meode aufgerufen werden sobald die Ausweichsprioritäten stegen|X |
| WayAnalyzer|avoidLeft()|Wird die Distanz und der Winkel des Lasers korrekt mitgegeben |X |
| WayAnalyzer|avoidLeft()| Entsprechend des mitgegebenen Laserwertes, müssen die Geschwindigkeiten entsprechend verändet werden (Nach links ausweichen und Vorfahrtgeschwindigkeit senken)|X |
| WayAnalyzer|avoidLeft()|Werden die errechnete Ausweichsgeschwindigkeiten per Broker an das "avoid" Topic übermittelt |X |
| WayAnalyzer|avoidRight()|Wird die Distanz und der Winkel des Lasers korrekt mitgegeben|X |
| WayAnalyzer|avoidRight()|Entsprechend des mitgegebenen Laserwertes, müssen die Geschwindigkeiten entsprechend verändet werden (Nach rehts ausweichen und Vorfahrtgeschwindigkeit senken)|X |
| WayAnalyzer|avoidRight()|Werden die errechnete Ausweichsgeschwindigkeiten per Broker an das "avoid" Topic übermittelt|X |
| WayAnalyzer|routeBlocked|Es muss in der vorgegeben Distanz ein Hindernis geziehlt abgefragt werden können  |0 |
|WayController|calcInOutCoord() | Es müssen von der Input Seite die Input- und die Outputkoordinaten berrechnte werden können |0|
|WayController|calcInOutCoord() | Es müssen von der Output Seite die Input- und die Outputkoordinaten berrechnte werden können |0|  
|WayController|calcInOutCoord() | Werden Koordinaten auf das "input" und das "Output" Topic gesendet |0|
|WayController|messageArrived() | Werden die Meldungen aus den Topics richtig ausgelesen und geparst |X|
|CrashController|crash() |Wird der Wert "true" zurückgegeben, sobald bumperControll() oder infraredSensoring() "true" zurückgeben|X|
| CrashController| bumperControl()|Es muss der Wert "true" zurückgegeben werden wen der Bumper mechanisch betätigt ist |X|
| CrashController| infraredSonsoring()|Es muss der Wert "true" zurückgegeben werden wen einer der InfrarotSensoren einen ungültigen Wert aufweist|X|
| Drive| goToTarget()|Der Robotino fährt auf die gewünschte Position und gibt "true" zurück. |X|
| Drive| explore()| Der Robotino fährt von einer Ecke zu anderen und sucht nach Kanten. Sobald er eine Hat wird diese angefahren.|X|
| Drive| approach()| Der Robotino fährt vor die MPS hin und gibt ein "true" zurück.|X|
| Drive| Ausweichen| Die Drive Klasse verarbeitet die Geschwindigkeiten die vom WayAnalyzer geschickt werden und weicht mit der entsprechnenden Geschwindigkeit aus.|X|


## Prüfverfahren WayAnalyzer
  
Der WayAnalyzer wurde auf einer Hindernisbahn Inbetriebgenommen und Überprüft auf dessen Funktion.
Die viselle Überprüfung wurde durch beobachten des Ausweichverhalten des Roboter geprüft. Die Arbeitswerte der Klassen und Methoden wurden mit Hilfe von Ausgabe der Konsole überprüft
  
## Prüfverfahren WayController, calcInOut()
  
Leider reicht die Zeit nicht mehr im Projektmanagement-Kurs den Softwarstand soweit zu bringen, dass die Koordinatenerechnungen In Betrieb genommen worden sind.
  
## Prüfverfahren CrashController
  
Der Crashcontroller wurde aufdessen Funktion überprüft, in dem man den Bumper betätigte oder ein Objekt vor jeden einzelnen der Infrarotsensoren hielt.

## Prüfverfahren Drive

Damit die Drive Klasse überprüft werden kann, müssen alle möglichen Szenarien simuliert werden. Die beinhaltet das Ausweichen, den Stopp und das Weiterfahren nach einem Crash.
  