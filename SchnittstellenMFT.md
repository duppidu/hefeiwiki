[Home](home)  
[Back](KonzeptMFT)  
***
### Quellen: 
[Symbol von Robotino](http://www.festo-didactic.com/ov3/media/customers/1100/robotinotopview_2.png)

***
## RefBox
![Schnittstellen_V2](https://gitlab.com/solidus/hefei/uploads/c5db7a69d20790bc0055eb0f092cb562/Schnittstellen_V2.png)

Im Diagramm oben sind die Schnittstellen der Refbox dargestellt. Das Internet diente dabei als Schnittstelle für das Besorgen von Informationen und Anleitungen. Alles was an wichtigen Informationen im Internet gefunden wurde, wurde fortlaufend ins GitLab Wiki geschrieben. Auf der VirtualBox liefen diverse Systeme. Ubuntu ist leichter zu bedienen und die Installation sollte laut Programmierer möglich sein. Die Funktion auf Fedora 18 wird auf der Downloadseite bestätigt. Der Programmierer selber hat die Refbox auf einem Fedora 20 am Laufen. Fedora 21 war zu dem Zeitpunkt die aktuellste Version. Pidora wurde versuchsmässig auf dem Mini-Computer Raspberry Pi ausprobiert. Letztendlich hat nur eine ältere Version auf einem Fedora funktioniert. Bei Ubuntu nicht einmal diese. Auf Pidora wurde nur die neueste getestet. Interessant wäre noch zu schauen, ob eine Version der Refbox, welche funktioniert, auf dem Raspberry laufen würde. Mit dem NetBeans wurde die ComRefBox programmiert und getestet. Das Programm wurde bei Änderungen auf das GitLab Git hochgeladen. Wenn bei den ersten Tests die ComRefBox auf dem NetBeans gestartet wurde, kommunizierte es mit der Refbox, dem zentralen und dem lokalen Broker. Am Cup musste die Klasse dann in das Programm des Roboters integriert werden. Im Bild oben wird diese Änderung mit gestrichelten Pfeilen dargestellt. Der Zugriff auf die Refbox, den zentralen und lokalen Broker geschieht direkt über den Roboter und nicht mehr über NetBeans.
***
### Laserscanner
Die einzigen Schnittstellen des Laserscanners sind im [Wayanalyzer](Wayanalyzer), im [Waycontroller](Waycontroller) und im [Drive](Drive). Da der Laserscanner [Singleton](Singleton) gemacht wird, kann der Laserscanner überall dort aufgerufen werden, wo er gebraucht wird.
***
### StateMachine

Die StateMachine kommuniziert ausschliesslich mit dem Broker. Auf verschiedenen Topics werden Messages empfangen. Auf anderen werden Befehle gesendet. Zu genaueren Informationen zu den Topics: [Mqtt Topics](MqttTopics)  

### PositionSet
Die Positionssetzung ist eine eigene Methode in der Klasse [Drive](Drive). Sie wird ausgeführt vom [Waycontroller](Waycontroller) auf den Befehl der [StateMachine](StateMachine) über den Broker.
### ColorDetection  

Die ColorDetection ist ein in sich geschlossener Prozess der nur gerade in der StateMachine aufgerufen wird und die Werte dann an den Broker schickt. 
