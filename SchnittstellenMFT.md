[Home](home)  
[Back](KonzeptMFT)  
***
## RefBox
![Schnittstellen](https://gitlab.com/solidus/hefei/uploads/4a7cd0b9b5cf1010b0687d039165404a/Schnittstellen.png)  
Im Diagramm oben sind die Schnittstellen der Refbox dargestellt. Das Internet diente dabei als Schnittstelle für das Besorgen von Informationen und Anleitungen.
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