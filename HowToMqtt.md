[Home](home) [Back](WikiSolidus)

# Inhalt  
- <a href="#lib">Library</a>
- <a href="#com">MQTT COM</a>
- <a href="#SM3">Setup-Assistent</a>
- <a href="#SM4">Gerät konfigurieren</a>  
***

## <a name="lib">Library  
Um dei MQTT Funktionen im Java zu verwenden, muss zuerst dien entsprechende
Library eingebunden werden  
Die Library kann [Hier](https://repo.eclipse.org/content/repositories/paho-releases/org/eclipse/paho/mqtt-client/0.4.0/mqtt-client-0.4.0.jar) Heruntergeladen Werden
Zudem muss sichergestellt werden, dass ein Mqtt Server im Netzwerk online ist mit vorteil mit einer [Festgelegten IP](http://jankarres.de/2013/09/raspberry-pi-statischefeste-ip-adresse-vergeben/)  
[Hier](MosquittoBroker) ist das Tutorial dazu.  
***

## <a name="com">MQTT COM  
In Unserem Projekt haben wir im Package Comm die Klasse MqttCom die enthaltenen Funktionen und Schritte zum aufbau der  
Kommunikation mit dem Broker werden hier in einzelnen Codeabschnitten erklärt. 

***
