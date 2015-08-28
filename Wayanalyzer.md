[Home](home)  
[Wiki](WikiSolidus)  

-----------------

# WayAnalyzer
Die Aufgabe des WayAnalyzers ist zu prüfen, ob sich keine Hindernisse auf dem optimalen Weg befinden. Dies wird erreicht, indem die Laserdaten einzeln durch eine trigonometrische Formel berechnet und verglichen werden. Diese Formel berechnet mittels Sinus und Cosinus die seitliche Entfernung zum Hindernis und vergleicht diese danach mit den eingestellten Parametern.
Sobald ein Hindernis erkannt wird, prüft das Programm auf welcher Seite es sich befindet und weicht  diesem entsprechend aus.
![WayAnalyzerFlowChart](https://gitlab.com/solidus/hefei/uploads/e4ca2986f7aa3470cca39c53ceac1a53/WayAnalyzerFlowChart.jpg) 

## Konstruktor
Der Konstruktor instanziiert die Kommunikation zum Broker, lädt die benötigten Parameter aus dem drive.xml und dem staticDistanceParams.xml-File und weist diese den Variablen zu. Aus dem drive.xml- File werden die Höchstgeschwindigkeit und die Infrarot-Mindestdistanzen ausgelesen. Aus dem staticDistanceParams.xml-File werden die Ausweichdistanz und die Banden-Offsets ausgelesen. Zudem werden die Anzahl der Laserpunkte, welche nacheinander ungültig sein müssen, festgelegt und die Schneisenbreite ausgelesen.

## Run
In der run()-Methode werden zyklisch die Laserwerte von 0° bis 270° eingelesen, der Weg bis zum Ziel wird errechnet und aktualisiert, und die aktuellen Koordinaten werden eingelesen. Ausserdem wird die avoidingDetector()-Methode aufgerufen, welche die Schneise überprüft.
![LaserArray](https://gitlab.com/solidus/hefei/uploads/51cc28feda4f1219ae5d6efe309c7889/LaserArray.jpg)
Auf der Graphik ist der Range des Lasersensors abgebildet. Es wird veranschaulicht von welchen physikalischen Positionen das Array mit Laserwerten befüllt ist. 

## AvoidingDetector
Der avoidingDetector() geht in einer while-Schlaufe für die linke Seite die Positionen vom 91° bis 180° und für die rechte Seite die Positionen 0° bis 89° durch.
Die Schlaufen beinhalten einen Vergleichs-Algorythmus, welcher den kleinsten gemessenen Laserwert speichert, sofern dieser nicht kleiner als 80 Integer( 80Int = 8cm) ist. Dieser Wert wird an die Ausweichs-Methoden (setAvoidSpeedLeft() oder setAvoidSpeedRight()) übergeben, sobald ausgewichen werden muss. In den Schlaufen wird als nächstes überprüft, ob sich ein Hindernis in der Schneise befindet. Sobald der Laser nacheinander mehrere ungültige Werte misst als vorgegeben sind, wird die Ausweich-Priorität um eins erhöht. Wird zwischen den ungültigen Werten ein gültiger Wert detektiert, wird der Counter zurück auf „0“ gesetzt. Diese Überwachung ist nötig, um Abweichungen der Laserdaten zu filtern. Wenn die Ausweich-Priorität auf einer Seite grösser als 0 ist, wird ausgewichen. Die Seite, die den höheren Wert aufweist, ist prioritär.


![Fahrschneise](https://gitlab.com/solidus/hefei/uploads/b8def5cc5948997301d36a09770d5fa6/Fahrschneise.jpg)
Die Distanz der Parameter aus dem staticDistanceParam.xml-File ist halb so gross wie die Verfahrschneise des Robotinos. Die rechte Seite wird von 0° bis 89° durchgearbeitet und mit Hilfe von trigonometrischen Formeln auf die Breite der halben Schneise überprüft. Die linke Seite wird von 91° bis 180° auf dieselbe Weise überprüft. Das wurde so gelöst, damit der Robotino nur Objekten in Fahrtrichtung ausweicht und nicht auch seitwärts weiter entfernten Objekten versucht auszuweichen.
Sobald auf eine Seite ausgewichen werden muss, wird überprüft, ob sich der Roboter weit genug vom Spielfeldende befindet, mittels checkLeftSide() und checkRightSide(), ob diese Seite frei ist und ob schon auf eine Seite ausgewichen wird.
Werden jedoch nur einzelne ungültige Punkte detektiert, bleibt die Ausweich-Priorität auf 0 und der Robotino fährt geradeaus weiter.

![AusweichsSituationen](https://gitlab.com/solidus/hefei/uploads/775de6a7d063e9d24b93477ef2481265/AusweichsSituationen.jpg)  

Diese Graphik visualisiert wie sich der Robotino zwischen komplexen Objektanordnungen hindurch manövriert.

![Routen](https://gitlab.com/solidus/hefei/uploads/306a7a149029c6c4239decf4f7198ace/Routen.jpg)

Diese Graphik deckt sämtliche Maschinenanordnungen ab, wie diese am Rande des Spielfeldes stehen können. Damit der Robotino nicht aus dem Spielfeld manövriert, wurde eine verbotene Zone vor den Spielfeldenden designt. Der Roboter darf diese verbotene Zone befahren, aber er darf nicht gegen die Bande ausweichen, sollte er ein Hindernis detektieren.
Die Distanz der Abstände zu dem Spielfeldrand können im staticDistanceParams.xml-File parametriert werden.
Blaue Rechtecke = MPS
Rote Zone = verbotene Zone

Sobald die setAvoidspeedLeft()- oder setAvoidspeedRight()-Methode die Ausweichgeschwindigkeit errechnet hat, wird verglichen ob sich seit dem letzten Zyklus die Geschwindigkeiten verändert haben.
Wenn sich diese verändert haben, wird die Speed-Klasse per Broker auf das "avoidingSpeed"-Topic gesendet. Ansonsten besitzt die Drive-Klasse bereits aktuelle Geschwindigkeitswerte.

## SetAvoidspeedLeft und Right
Die setAvoidspeed Methoden werden aufgerufen, wenn auf der entgegengesetzten Seite ein Hindernis detektiert wurde. Sie überprüfen anhand des mitgegebenen Laserwertes und dessen Winkel, wie schnell ausgewichen werden muss. Desto näher das Hindernis ist, desto schneller wird ausgewichen und die Vorwärtsgeschwindigkeit stärker verzögert. Ist das Hindernis zu weit entfernt, werden die aktuellen Geschwindigkeiten beibehalten.
Die Ausweichgeschwindigkeit wird mittels einer Formel berechnet. Da am Robocup 2015 in Hefei eine zweite Formel entwickelt, aber nicht getestet wurde, befindet sich die Beschreibung dessen im Code selbst. 

## CheckLeftSide
Sobald der Robotino einem Objekt ausweicht, bewegt sich dieser seitwärts. Um zu überprüfen ob sich ein Objekt auf der linken Seite im Weg befindet wird die Methode checkLeftSide() verwendet. Die Überprüfung wird folgendermassen durchgeführt: Bevor der Roboter links ausweicht, wird diese Methode aufgerufen. Durch eine while-Schlaufe werden die Positionen 165° bis 195° fortlaufend auf einen im staticDistanceParams.xml-File parametrierbaren Wert verglichen. Sobald mehr als der parametrierte Wert aufeinander folgende, unzulässige Laserwerte entdeckt werden, gibt die Methode den Wert„true“ zurück. Dieser Vergleichsalgorithmus basiert auf demselben Algorithmus wie ihn der avoidingDetector() ebenfalls verwendet.

![checkLeftSide](https://gitlab.com/solidus/hefei/uploads/a4a7ce30edadf7fa82bce4a2c923581c/checkLeftSide.jpg)
Visualisierung wie der Robotino vor dem Ausweicheprozess nach links, die linke Seite überwacht.

## CheckRightSide
Sobald der Robotino einem Objekt ausweicht, bewegt sich dieser seitwärts. Um zu überprüfen ob sich ein Objekt auf der rechten Seite im Weg befindet wird die Methode checkRightSide() verwendet. Die Überprüfung wird folgendermassen durchgeführt: Bevor der Roboter rechts ausweicht, wird diese Methode aufgerufen. Durch eine while-Schlaufe werden die Positionen -15° bis 15° fortlaufend auf einen im staticDistanceParams.xml-File parametrierbaren Wert verglichen. Sobald mehr als der parametrierte Wert aufeinander folgende, unzulässige Laserwerte entdeckt werden, gibt die Methode den Wert„true“ zurück. Dieser Vergleichsalgorithmus basiert auf demselben Algorithmus wie ihn der avoidingDetector() ebenfalls verwendet.

![checkRightSide](https://gitlab.com/solidus/hefei/uploads/c0be0bb827687b76779b343bcf73f0d5/checkRightSide.jpg)
Visualisierung wie der Robotino vor dem Ausweicheprozess nach rechts, die rechte Seite überwacht.

## InfraredSensoring
Diese Methode vergleicht alle Infrarotsensoren, welche rund um den Robotino angebracht sind. Wird der Wert einer dieser Sensoren kleiner als der parametrierte Wert, so wird in die entgegengesetzte Richtung ausgewichen. Beim vordersten Infrarot Sensor wurde eine separate Distanz als parametrierter Wert gewählt, da dieser physikalisch nach hinten versetzt wurde.

![InfraredSensoring](https://gitlab.com/solidus/hefei/uploads/23ce961af647471aeccb24bc0e90af83/InfraredSensoring.jpg)
Die Graphik visualisiert, in welche Richtung der Robotino ausweicht, wenn ein oder mehrere Infrarotsensoren einen ungültigen Wert aufweisen.
Blauer Pfeil  = Fahrtrichtung  
Rote Strahlen = Infrarot-Sichtfeld

