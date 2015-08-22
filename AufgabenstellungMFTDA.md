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

#### Refbox
Das Thema sollte eigentlich sinnvollerweise in zwei unterschiedlichen Themen aufgeteilt werden. Zum einen die Klasse "ComRefBox", welche eine Verbindung zur Refbox herstellt. Zum anderen die Refbox selber. Da diese aber oft zusammenspielen, wird darauf verzichtet. Zuerst soll die alte Refbox auf einem Linux-System zum Laufen gebracht werden. Mit den Daten vom letzten Jahr wird danach die Kommunikation getestet. Wenn alles funktioniert kann die Refbox auf den neusten Stand gebracht und die neuen Daten eingebunden werden. Die Klasse muss noch angepasst und verbessert werden. Zudem fehlen weitgehendst noch die Kommentare und die Javadoc. 

#### RobotinoOS
Der Robotino soll mit der neuesten Firmware ausgestattet werden. Auf das System müssen des weiteren alle benötigten Programme installiert werden. Zur Sicherheit und zur Abgleichung der verschiedenen Robotinos soll vom fertig aufgesetzten Robotino ein Image gemacht werden. Das Ziel des Images ist, dass es innert weniger Minuten auf einen Robotino geladen werden kann und bei Änderungen auch möglichst schnell ein neues Image erstellt werden kann. 

#### ColorDetection

Die Farbdedektierung muss stabilisiert werden und dann während des Cups neu eingestellt werden.  
Das immer noch anstehende Device Problem muss behoben werden. 

#### MarkerDetection

Es muss sich in die Klasse eingelesen werden um sie in einem Fehlerfall während des Cups anpassen zu können.