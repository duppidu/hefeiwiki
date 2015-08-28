[Home](home)  
[DokuSolidus](DokuSolidus)  
[Konzept](KonzeptBKDA)  

----------

# Analyse
## Inhalt  

- Gedanken
- Materiell
- Ergebnis

## Gedanken
### WayAnalyzer:
Die Formel, die die Geschwindigkeiten berechnet, muss gut durchdacht werden, damit die Testphase kurz gehalten werden kann. Auch einzelne Spezialfälle müssen behandelt werden.
zum Beispiel: 
- Der Robotino soll beim Ausweichen das Spielfeld nicht verlassen.
- Der Robotino darf während dem seitwärts Ausweichen keine Kollision mit Objekten verursachen.
- Der Robotino muss erkennen, ob eine Lücke zwischen den Hindernissen, befahrbar ist oder nicht.

Diese Spezialfälle müssen einzeln getestet werden.
### WayController:
Der WayController muss die Anforderungen der Produktions Phase an die Drive Klasse weitergeben können. Hierzu müssen einige Casefälle erstellt oder erweitert werden.
Einige Änderungen, welche programmiert werden müssen, sind:
- Im approach Case soll anhand der Spielphase erkannt werden ob die Input und Output Positionen berechnet werden müssen oder ob die Positionskoordinaten des Robotinos zurückgesetzt werden müssen. Hierfür muss die Spielphase von dem Broker empfangen werden.
- Damit alle Positionen einer MPS Station angefahren werden können, müssen weitere approachCasefälle programmiert werden, welche einen unterschiedlichen Übergabewert enthalten.

Um die Input- und Outputkoordinaten einer MPS zu berechnen werden trigonometrische Formeln eingesetzt.
### Drive
Um die zusätzlichen Positionen an den Capstations und an den Ringstations anfahren zu können, müssen wir mit dem Produktionsteam eine Möglichkeit finden, wie sie uns mitteilen wollen, an welche Maschinenposition zu fahren ist. Anschliessend können wir die approach Methode entsprechend anpassen und testen.
## Materiell
### WayAnalyzer:
Um den Fahrverlauf zu testen, wird ein Versuchsaufbau benötigt. Der Versuchsaufbau soll die Ausweichsituationen simulieren, so wie diese am Robocup auftreten werden. Die Ausweichdynamik soll im Solidus-Raum mit Hilfe unseres MPS-Nachbaus und einigen Kartonkisten getestet werden. 
### WayController:
Anhand der Nachrichten, welche auf dem „actions“ Topic empfangen werden, muss der WayController unterscheiden können, welche Positionen an der MPS angefahren werden müssen. Der Inhalt dieser Nachrichten wird mit dem Produktionsteam abgesprochen und danach in der Dokumentation festgehalten.
Damit die Koordinaten korrekt berechnet werden, müssen alle Situationen, die auftreten können, skizziert werden. Aus diesen Skizzen werden danach die trigonometrischen Formeln, welche die Positionen berechnen, erstellt. Diese Positionen werden anschliessend an den Broker gesendet.
### Drive
Die überarbeitete approach Methode kann getestet werden, indem die entsprechende Nachricht auf das „actions“ Topic gesendet wird. Der Robotino sollte danach an die entsprechende Offsetposition fahren.
## Ergebnis
### WayAnalyzer:
Der Roboter soll die Zielkoordinaten erreichen ohne dabei ein Hindernis zu berühren. Die Hindernisse müssen umfahren werden ohne dass der Zielpunkt verloren geht. Der Einfluss der Fahrdynamik soll per Broker an die Drive Klasse weitergegeben werden.
Diese Tests schliessen ein:
- Komplexe Hindernisanordnungen umfahren.
- Während dem seitwärts Ausweichen mit keinem Objekt kollidieren.
- Ausweichgeschwindigkeit dynamisch regulieren.
- Das Feld darf während eines Ausweich-Vorgangs nicht verlassen werden. 
- Zu kleine Lücken erkennen und weiter ausweichen. Die komplexen Hindernisanordnungen sind im technischen Wiki unter WayAnalyzer ersichtlich.

### WayController:
Der WayController beachtet die aktuelle Spielphase, indem diese vom Broker empfangen wird. Anhand der Spielphase wird entschieden, ob die Position des Robotinos zurückgesetzt wird oder die Input- und Outputkoordinaten berechnet werden.
Ebenfalls enthält die Nachricht auf dem „actions“ Topic die Information, welche Position die approach Methode anfahren muss. Sobald sich der Robotino vor dem Band befindet und die approach Methode der Drive Klasse ein True zurück gibt, werden die entsprechenden Positionen der MPS berechnet und auf den Broker gesendet oder die Position zurückgesetzt. Während der Explorationsphase werden die Koordinaten der MPS berechnet und während der Spielphase werden die Koordinaten jeweils zurückgesetzt.
### Drive
Durch den Übergabewert wird ein Offset, der aus einem Config-File gelesen wird, der aktuellen Position dazu gerechnet. Danach soll der Robotino auf das neue Ziel fahren und die MPS anfahren.
