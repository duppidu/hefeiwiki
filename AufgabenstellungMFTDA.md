[Home](home)  
[Back](KonzeptMFT)  

----------

### Inhalt ###

- Allgemein
- Spezifisch

----------

### Allgemein ###

In der Diplomarbeit haben wir die Aufgabe uns auf den [Robocup 2015](http://www.robocup2015.org/) in [Hefei](https://www.google.ch/maps/place/Hefei,+Anhui,+China/@31.8555246,117.2862625,11z/data=!3m1!4b1!4m2!3m1!1s0x35cb640ef207cf9d:0xdc151173f2c33299) vorzubereiten und diesen erfolgreich zu beenden.
Wir nehmen an der [Logistics Laegue](http://www.robocup2015.org/show/article/14.html) teil.  
Unsere Aufgabe besteht darin:  
- In einem vordefinierten Feld, 6 Maschinen zu erkennen und diese der [RefBox](WikiSolidus) zu melden.
- Von der [RefBox](WikiSolidus) erhaltene Produktionsaufträge selbständig abzuwickeln.    
 


----------

### Spezifisch ###

#### Laserscanner
Die Aufgabenstellung in diesem Bereich besteht darin, den bestehenden Code so zu erweitern, dass er für unsere Aufgabe nützlich ist.  
- Erkannte Kanten auswerten
- Weitere [Filter](Laserscanner) hinzufügen
- Anfahrpunkt und Anfahrwinkel vor der Maschine berechnen
- Distanzwerte zur Verfügung stellen ([Wayanalyzer](Wayanalyzer), [PositionSet](PositionSet))
- Erkennen ob sich eine Maschine auf dem Feld befindet


#### StateMachine
Die [StateMachine](StateMachine) muss mindestens die Setupphase und die Explorationsphase vollständig handeln können. Für die Produktionsphase ist ein grobes Gerüst vorgesehen.

#### PositionSet
Die Positionssetzung im Startbereich soll mithilfe des Laserscanners erfolgen. Die Robotinos sollten am Anfang nur ungefähr genau in den Startbereich gesetzt werden müssen. Die Genauigkeit soll so hoch wie möglich gewährleistet sein. Trotzdem muss ein guter Mittelweg zwischen Genauigkeit und Geschwindigkeit gefunden werden.

#### ComRefbox
Das Thema sollte eigentlich sinnvollerweise in zwei unterschiedlichen Themen aufgeteilt werden. Zum einen die Klasse "ComRefBox", welche eine Verbindung zur Refbox herstellt. Zum anderen die Refbox selber. Da diese aber oft zusammenspielen, wird darauf verzichtet. Wenn das Schiedsrichterprogramm von der deutschen Uni gemeint ist, wird es Refbox genannt. Falls es die Klasse ist die ausprogrammiert werden soll, wird es "ComRefBox" genannt.

>**Aufgabenstellung für das Prozessmodul**  
>*"Zuerst soll die alte Refbox auf einem Linux-System zum Laufen gebracht werden. Mit den Daten vom letzten Jahr wird danach die Kommunikation getestet. Wenn alles funktioniert kann die Refbox auf den neusten Stand gebracht und die neuen Daten eingebunden werden. Die Klasse muss noch angepasst und verbessert werden. Zudem fehlen weitgehendst noch die Kommentare und die Javadoc."*

Die aktuellste Version der Refbox konnte bis jetzt nicht zum Laufen gebracht werden. Eine Installation, welche aber bereits über 2 Monate alt ist, funktioniert teilweise. Die neuesten Proto-Files und die neue API konnten bereits im NetBeans eingebunden werden. Die Kommunikation mit der älteren Installation funktioniert soweit, dass alle nötigen Informationen für die Durchführung einer Explorationsphase abgerufen werden können. 
Hauptziel ist nun die Entwicklung der Klasse "ComRefBox". Es ist bereits viel Zeit für das Aufsetzen einer Refbox verloren gegangen. Es ist wichtig jetzt die Programmierung voranzutreiben, sodass mindestens eine Explorationsphase durchgeführt werden kann. Das Aufsetzen der Refbox wird als Nebenziel gesetzt. Für den Test des Programms steht diese ältere Version der Refbox zur Verfügung.

#### RobotinoOS
>**Aufgabenstellung für das Prozessmodul**  
>*"Der Robotino soll mit der neuesten Firmware ausgestattet werden. Auf das System müssen des Weiteren alle benötigten Programme installiert werden. Zur Sicherheit und zur Abgleichung der verschiedenen Robotinos soll vom fertig aufgesetzten Robotino ein Image gemacht werden. Das Ziel des Images ist, dass es innert weniger Minuten auf einen Robotino geladen werden kann und bei Änderungen auch möglichst schnell ein neues Image erstellt werden kann."*

Für das Robotino OS ist bereits alles soweit vorbereitet. Nun muss vor der Reise noch ein aktuelles Image gemacht werden. Am Cup muss dieses dann auf jeden einzelnen Roboter aufgespielt werden. 

#### ColorDetection

Die Farbdedektierung muss stabilisiert werden und dann während des Cups neu eingestellt werden.  
Das immer noch anstehende Device Problem muss behoben werden. 

#### MarkerDetection

Es muss sich in die Klasse eingelesen werden um sie in einem Fehlerfall während des Cups anpassen zu können.