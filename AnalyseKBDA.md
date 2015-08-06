[Home](home)  
[DokuSolidus](DokuSolidus)  
[Konzept](KonzeptBKDA)  

----------

## Inhalt  

- Gedanken
- Materiell
- Ergebnis

## Gedanken 
  
### WayAnalyzer:  
  
Die Formel die die Geschwindigkeiten berechnet muss gut durchdacht werden, damit die Testphase kurz gehalten wird. Auch einzelne Spezialfälle müssen behandelt werden können.  
zum Beispiel:  
- Der Robotino soll beim Ausweichen das Spielfeld nicht verlassen.  
- Der Robotino darf während dem seitwärts Ausweichen keine Kollision mit Objekten verursachen.  
- Der Robotino muss erkennen ob eine Lücke zwischen den Hindernissen befahrbar ist oder nicht.

Diese Spezialfälle müssen einzeln getestet werden.
  
### WayController:  
Der WayController muss die Anforderungen der Produktions Phase an die Drive Klasse weitergeben können. Hierzu, müssen einige Casefälle erstellt oder erweitert werden.  
Einige Änderungen welche aus programmiert werden müssen sind:
- Im approach Case soll anhand der Spielphase erkannt werden ob die Input und Output Positionen berechnet werden müssen oder ob die Position des Robotinos zurückgesetzt werden muss. Hierfür muss der Spielstand vom Broker empfanden werden.
- Damit alle Positionen einer MPS Station angefahren werden können, müssen weitere approach Casefälle programmiert werden, die einen unterschiedlichen Übergabewert enthalten.

Um die Input- und Outputkoordinaten einer MPS zu berechnen wird die Trigonometrie eingesetzt.

### Drive

Um die zusätzlichen Positionen an den Capstations und Ringstations anfahren zu können müssen wir mit dem Produktionsteam eine Möglichkeit finden wie sie und dieses mitteilen. Danach können wir die approach Methode anpassen und testen.
  
## Materiell  
  
### WayAnalyzer:  
  
Um den Fahrverlauf aus zu testen wird ein Versuchsaufbau benötigt. Der Versuchsaufbau soll Ausweichsituationen simulieren, so wie diese am Robocup ebenfalls auftreten werden. Die Ausweichdynamik soll im Solidus-Raum mit Hilfe unserer MPS und einigen Kartonkisten ausgetestet werden.  

### WayController:  

Anhand der Nachrichten die auf dem actions Topic ankommen muss der WayController unterscheiden können welche Positionen an der MPS angefahren werden müssen. Diese Nachrichten werden mit dem Produktionsteam abgesprochen und danach in der Dokumentation festgehalten.
Damit die Koordinaten korrekt berechnet werden können müssen alle Situationen die auftreten können skizziert werden. Aus diesen Skizzen werden danach die trigonometrischen Formel, die die Positionen berechnen, erstellt. Diese Positionen werden anschliessend an den Broker gesendet.

### Drive
Die überarbeitete approach Methode kann getestet werden indem die entsprechende Nachricht auf das actions Topic gesendet werden. Der Robotino sollte danach an die entsprechende Offsetposition fahren.
  
## Ergebnis  
  
### WayAnalyzer:  
  
Der Roboter soll die Zielkoordinaten erreichen ohne dabei ein Hindernis zu berühren. Die Hindernisse, müssen Umfahren werden können ohne das der Zielpunkt verloren geht. Der Einfluss der Fahrdynamik, soll per Broker an die Drive Klasse weitergegeben werden.  
Diese Tests schliessen ein:
- Komplexe Hindernisanordnungen umfahren.
- Während dem seitwärts ausweichen mit keinem Objekt kollidieren.
- Ausweichgeschwindigkeit dynamisch regulieren.
- Das Feld darf während eines Ausweich-Vorgang nicht verlassen werden. 
- Zu kleine Lücken erkennen und weiter ausweichen.
Die komplexen Hindernisanordnungen sind im technischen Wiki unter WayAnalyzer ersichtlich.
  
  
### WayController:  
 
Der WayController beachtet die aktuelle Spielphase indem diese vom Broker empfanden wird. Anhand dessen wird entschieden ob die Position des Robotinos zurückgesetzt wird oder die Input- und Outputkoordinaten berechnet werden. Ebenfalls enthaltet die Nachricht auf dem actions Topic die Information welche Position die approach Methodeanfahren muss.
Sobald sich der Robotino vor dem Band befindet, wenn die approach Methode der Drive Klasse ein True zurück gibt, werden die entsprechenden Positionen der MPS berechnet und auf den Broker gesendet. 
  

### Drive

Durch den Übergabewert wird ein Offset, der aus einem Konfig File gelesen wird, der aktuellen Position dazu gerechnet. Danach soll der Robotino auf das neue Ziel fahren und die MPS anfahren.

  