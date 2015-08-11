# Color Detection  
 
## Aufruf  

Die ColorDetection wird in einem separaten .jar File gestartet.  
Dies hat folgende Gründe:
- mit OpenCV unter Java war es nicht möglich die Kamera-Verbindung zu trennen.  
- mit dauerhaft laufender Kamera machte das C++ Programm zur Markererkennung Probleme mit der Device Auswahl.  
     
Der Aufruf wir in der [StateMachine](StateMachine) mit dem Befehl       
Runtime.getRuntime().exec(new String[]     
                    {  
                        "java", "-jar", "/home/robotino/hefei/ColorDetection.jar"  
                    });    
Durch diesen wird ein neuer Prozess gestartet.  
  
## Grundlegender Programmablauf 
Beim instanzieren des Programms wird die Kamera gestartet und das Kamera-bild auf eine Matrix gelegt.
  

Nun wird in der run() Methode trackColor gestartet.  

Die Methode trackColor() wird nun 40 mal für jede Farbe im 50ms Takt aufgerufen.   
Beim überprüfen wir nur Leuchten detektiert, zum eingrenzen welche Lampe das leuchtet wird die Position des lichtes überprüft.  
  
Nachdem jede Farbe überprüft wurde wird in lightAnalyze() analysiert wie oft Licht in dem entsprechenden Feld detektiert wurde.  
  
 **Nicht Leuchten**  
Wird in unter 10% der Fälle Licht detektiert giltet die Lampe als nicht Leuchtend.  
  
**Blinken**  
Wir in ca der hälfte der Fälle Leuchten dedektiert blinkt die Lampe.  
  
**Leuchten**  
Wird in ca 90% der Fälle Leuchten detektiert Leuchtet die Lampe.  
  
     
    
   
![Diagramm](https://gitlab.com/solidus/hefei/uploads/1354c7f2143496a12a9e465143b67e62/Diagramm.JPG)  
    
### Farberkennung   
  
Die Farbdedektierung wird in 2 Bildern gemacht, zum einen im normalen Bild in RGB und zum andren im HSV konvertierten Bild. Nach dem Starten der Kamera muss das Programm mindestens 5 Sekunden Pausieren da sie in dieser Zeit noch fokussieren muss 
  
#### HSV  
  
Alle Farben werden in HSV definiert. HSV ist ein Farbcode der in 3 Zahlen angeben wird.    
  
![HSV_color_space](https://gitlab.com/solidus/hefei/uploads/8028743baa238d7c90889414cbefa423/HSV_color_space.png)
![HSV_cone](https://gitlab.com/solidus/hefei/uploads/fc0c1707ccb3c582bcb3fbac5aaf187b/HSV_cone.jpg)
  
  
- Die erste Zahl gibt durch einen Winkel an um welche Farbe es sich handelt  
- Die zweite Zahl definiert die Sättigung der Farbe
- Die dritte Zahl definiert die Helligkeit         
      

       
Die Farbe wird in ein Scalar gespeichert in diesem können die drei Werte in einem bereich von 0-255 gespeichert.   
Das bedeutet dass die Werte konvertiert werden müssen sprich für die Farbe 360° = 255 und in der Sättigung und Helligkeit 100% = 255.  	

#### Vorgegen zur Suche einer Farbe  

Mit Hsv_min und Hsv_max wird die Farbe definiert. Im unkonvertierten Bild wird nun überprüft welche Farbe in der Toleranz von Hsv_min und max liegt danach wird das Bild in ein HSV Bild Konvertiert und die gleiche überprüfung mit Hsv2_min und Hsv2_max gemacht.  
Nach dieser Überprüfung vergleicht das Programm in Welchen Bereichen beide Überprüfungen übereinstimmen. Somit hat man dann eine genaue Farbsuche.

#### Bereichseinschränkung

Um den Bereich festzulegen in dem das Programm suchen soll werden zuerst in Jeden gefundenen Farbbereich Linien gezeichnet dies geschieht über die Methode  Imgproc.HoughLinesP()     
Nach dem einzeichnen wir durch eine Schlaufe die Daten aller gefundenen Linien ausgelesen. In diesen Daten befinden sich dann auch Informationen zu den Positionen der Eckpunkte der Linien in X und Y.  
Mit einer einfachen If() Bedingung wird dann die Position eingegänzt.  

![AbendPlayoffs1](https://gitlab.com/solidus/hefei/uploads/6a7e1d7b544066d7107dbe91131a0d6b/AbendPlayoffs1.JPG)

Die blauen Bereiche auf dem Bild sind die erkannten Farbberieiche. Falls nun eine Farbe im Suchbereich ist wird in diesen schwarze Linien gezeichnet wie auf diesem Bild in der grünen Lampe ersichtlich ist.
  
  
  
Falls nun nach 40 Überprüfungen jeder Farbe keine als Leuchten gemeldet wurde wird der Bereich nun um 40 Pixel (ein halbes grünes Häuschen) nach links und falls da immer noch nichts erkennt wird noch nach rechts verschoben.  

#### Spezialfall Deliveristation

Das Programm überprüft vor jeder Dedektierung um was für einen Maschinen Typ es sich handelt. Steht der Robotino vor einer DS muss der Suchbereich geändert werden da die Position der Lampe der DS nicht am gleichen Ort ist wie bei den anderen Maschinen.  
Der Maschinen Typ wird mit der Broker Methode messageArrived() ausgelesen.  

![PositionDS](https://gitlab.com/solidus/hefei/uploads/f4c408249ac2560dcbe2bf5acc9aa119/PositionDS.JPG)  
 
Verschobene Position der DS.

