[Home](home)   
[Back](DokuSolidus)   

***

## Testplan

**Situation:**  Eine Explophase mit der Erkennung von 2 Maschinen soll getestet werden.

| Klasse|  Beschreibung| Resultat | I.O.| 
| :------- | --- | --- | :---- |
| Start-Up|Start-Up ruft Statemaschine auf |Funktioniert|X |
| Statemaschine|Nullen|Konntet noch nicht getestet werden | 0 |
| Statemaschine|goToTarget aufs Feld|Konnte noch nicht getestet werden|0 |
| Drive|Fährt auf das Feld| goToTarget Funktioniert somit wird er auch fahren |X |
| Statemaschine| ruft Explokonroller auf und schickt Felder| Funktioniert |X |
| Explokontroller|gibt dem Drive die Werte der Zone in der Explort werden muss|Funktioniert |X |
| Drive|Fährt zu erster Zone|Funktioniert|X |
| Laser|Suchen nach Kanten|Kannten werden erkannt|X |
| Drive|Ausrichten|Robotino richtet sich aus|X |
| TagErkennung|Die Kamera muss das Tag erkennen|Funktioniert über weite distanzen|X |
| Lampenerkennung|Soll den Wert der Lampe überprüfen und senden|Funktioniert|X |
| Drive|Fahre in nächste Zone|Funktioniert noch nicht sauber da wir das Ausweichen noch nicht testen konnten|0 |
| Ausweichen|Robotino soll zuverlässig Objekten ausweichen|Konnte leider noch nicht getestet werden da wir keinen funktionstüchtigen Robi hatten|0 |



## Resultat  

Die ExplorationsPhase erwies sich als schwieriger als erst angenommen. Ende PM Kurs ist es uns jedoch möglich 2 Maschinen zu entdecken und diese abzuspeichern. 
Leider konnten wir nicht all unsere Ziele vom PM erfüllen da sich einige unerwartete Probleme auftraten. Beispielsweise das Ausweichen des Robotinos erwies sich als schwieriger als angenommen. Ebenfalls wurde die Problematik mit der Refbox noch nicht behoben.  
Das herstellen eines ersten Produktes war ein zu hohes Ziel und wird jetzt in der nächsten Projektphase der Diplomarbeit weiterverfolgt.

### Teilziele:
| Teilziel| Resultat |
| :------- | --- |
| Der Start-Up Fall muss ausprogrammiert sein.| Start-Up ist bis zum aktuellen Stand ausprogrammiert |
| Driveklassen müssen funktionstüchtig und fehlerfrei arbeiten | Sind ausprogrammiert |
| State-Machine muss funktionsbereit sein | State-Machine ist auf dem aktuellen Stand|
| Zentralbroker muss Kommunikation zwischen Robotinos ermöglichen | Zentraler Broker ist eingerichtet |
| Restart-Funktion um Java-Programm neu zu starten | Restart wurde noch nicht angegangen |
| Robotino mechanisch komplett mit Greifer und Lösung für Bauteil abgriff | Die Teile sind fertig gedruckt und zusammengesetzt |
| Jeder Programmteil muss über ein angemessenes Diagramm verfügen (Klassendiag, Sequencediag, etc…) | Jeder hat sein Diagramm erstellt|
| Cupvorbereitungen müssen getroffen sein (Packlisten, Materialisten, Finanzierungen, Impfungen) | Listen wurden erstellt und Abklärungen getroffen |
| Refbox muss funktionieren | Refbox ist noch nicht soweit |