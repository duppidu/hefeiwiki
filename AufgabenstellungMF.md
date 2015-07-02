[Home](home) [Back](KonzeptMF)  

----------

### Inhalt ###

- Allgemein
- Spezifisch

----------

### Allgemein ###

In dem Kurs 6.492 PM (Process Modul) haben wir die Aufgabe, uns auf den [Robocup 2015](http://www.robocup2015.org/) in [Hefei](https://www.google.ch/maps/place/Hefei,+Anhui,+China/@31.8555246,117.2862625,11z/data=!3m1!4b1!4m2!3m1!1s0x35cb640ef207cf9d:0xdc151173f2c33299) vorzubereiten.
Wir nehmen an der [Logistics Laegue](http://www.robocup2015.org/show/article/14.html) teil.  
Unsere Aufgabe besteht darin:  
- In einem vordefinierten Feld, 6 Maschinen zu erkennen und diese der [RefBox](WikiSolidus) zu melden.
- Von der [RefBox](WikiSolidus) erhaltene Produktionsaufträge selbstständig abzuwickeln.    
 


----------

### Spezifisch ###

#### Laserscanner
Die Aufgabenstellung in diesem Bereich bestand darin, den bestehenden Code so zu erweitern, dass er für unsere Aufgabe nützlich ist.  
- Erkannte Kanten auswerten
- Weitere [Filter](Laserscanner) hinzufügen
- Anfahrpunkt und Anfahrwinkel vor der Maschine berechnen
- Distanzwerte zur Verfügung stellen ([Wayanalyzer](Wayanalyzer), [PositionSet](PositionSet))


#### StateMachine
Die [StateMachine](StateMachine) muss immer mindestens so weit ausgebaut sein, dass der aktuelle Codeteil ausgeführt werden kann. 
#### Refbox
Das Thema sollte eigentlich sinnvollerweise in zwei unterschiedlichen Themen aufgeteilt werden. Zum einen die Klasse "ComRefBox", welche eine Verbindung zur Refbox herstellt. Zum anderen die Refbox selber. Da diese aber oft zusammenspielen, wird darauf verzichtet. Zuerst soll die alte Refbox auf einem Linux-System zum Laufen gebracht werden. Mit den Daten vom letzten Jahr wird danach die Kommunikation getestet. Wenn alles funktioniert kann die Refbox auf den neusten Stand gebracht und die neuen Daten eingebunden werden. Die Klasse muss noch angepasst und verbessert werden. Zudem fehlen weitgehendst noch die Kommentare und die Javadoc. 
#### RobotinoOS
Der Robotino soll mit der neuesten Firmware ausgestattet werden. Auf das System müssen des weiteren alle benötigten Programme installiert werden. Zur Sicherheit und zur Abgleichung der verschiedenen Robotinos soll vom fertig aufgesetzten Robotino ein Image gemacht werden. Das Ziel des Images ist, dass es innert weniger Minuten auf einen Robotino geladen werden kann und bei Änderungen auch möglichst schnell ein neues Image erstellt werden kann. 

----------