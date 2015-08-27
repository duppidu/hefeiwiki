[Home](home) [Back](WikiSolidus)


Raspberry Pi als MQTT Broker
===================

#### Inhalt
- <a href="#in">Installation</a>
- <a href="#mq">MQTT.fx</a>

Wir Verwenden während des Robocps zusätzlich zu den Robotinos 2 Raspberry Pi
Die Raspberry Übernehmen folgende Aufgaben:
> - Zentraler MQTT Broker für die Kommunikation der Robotinos
> - Lokales GitLab Während des Cups (zur unabhängigkeit vom Internet)




## <a name="in">Installation
Vor der Installation Bringen wir die Software auf dem Raspberry auf den neusten Stand
```
sudo apt-get update
sudo apt-get upgrade
```
Nachdem der Upgrade-Befehl ausgeführt wurde Wird nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ] 
Mit J und Enter bestätigen  


#### Nun Installieren wir [Mosquitto](http://mosquitto.org/) auf dem Raspberry:
```
sudo apt-get install mosquitto
```
Ist Mosquitto bereits Installiert wir dies angezeigt:
mosquitto ist schon die neueste Version  

Ist das Programm nicht installiert: 
wird wider nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ]

Der Broker Läuft nach der Installation im Hintergrund unsichtbar weiter
mit den Folgenden Kommandos kann er jedoch gesteuert werden.
```
sudo service mosquitto status
sudo service mosquitto stop
sudo service mosquitto start
sudo service mosquitto restart
```

Sollte dies nicht Funktionieren kann anstatt
```
sudo service mosquitto (Kommando)
```
auch
```
sudo /etc/init.d/mosquitto (Kommando)
```
verwendet werden
Damit wird ein File angegeben welches mit den jeweiligen Kommandos arbeitet
und so zu sagen als xy.exe funktioniert. (kann durch cat (filenamen) angeschaut werden)


## <a name="mq">MQTT.fx
Um den Verlauf des Brokers im Windows zu verfolgen, werwenden wir das Programm [MQTT.fx](http://mqttfx.jfx4ee.org/)
welches [hier](http://mqttfx.jfx4ee.org/index.php/download) heruntergeladen werden kann.


![MQTT_normal](https://gitlab.com/solidus/hefei/uploads/a1f9093c81be329464f6b2b3f4639c50/MQTT_normal.PNG)

Durch das drücke des Zahnrades oben neben dem Connect Button können die Einstellungen aufgerufen werden 

![MQTT_Einstellungen](https://gitlab.com/solidus/hefei/uploads/fc23289a0f0d22940460cd05d170575e/MQTT_Einstellungen.PNG)

Wichtig auf dieser Seite Ist die Eingabe von
>- Profile Name:  z.B   Robotino1
>- Broker Address: z.B  172.26.1.1
>- Broker Port:   meist 1883
>- Client ID: Nikname oder Name

Um Den Gebrauch von zu vereinfachen, können die Punkte Publish, Subscribe, Scripts, Broker Status, Log vom Hauptfenster gelöst werden

![MQTT_geloest](https://gitlab.com/solidus/hefei/uploads/2bcd22efc9341ab68564155e439a0cc8/MQTT_geloest.PNG)

Das Letzte was zum betrachten der gesendeten Nachrichten noch fehlt, ist das Subscriben.

>-als erstes in der Liste unter Connect auf  Subscribe wechseln.
>-neben dem Subscribe button den frei definierbaren [Topic](MqttTopics) Eingeben
>-auf Subscribe drücken
>-für jeden gewollten [Topic](MqttTopics) widerholen




