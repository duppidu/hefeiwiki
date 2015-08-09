## <a name="lib">Library</a>  
Um dei MQTT Funktionen im Java zu verwenden, muss zuerst die entsprechende
Library im Netbeans eingebunden werden  
Die Library kann [Hier](https://repo.eclipse.org/content/repositories/paho-releases/org/eclipse/paho/mqtt-client/0.4.0/mqtt-client-0.4.0.jar) Heruntergeladen Werden
Zudem muss sichergestellt werden, dass ein Mqtt Server im Netzwerk online ist mit vorteil mit einer [Festgelegten IP](http://jankarres.de/2013/09/raspberry-pi-statischefeste-ip-adresse-vergeben/)  
[Hier](MosquittoBroker) ist das Tutorial dazu.  
***

## <a name="com">MQTT COM  </a>
In Unserem Projekt haben wir im Package Comm die Klasse MqttCom die enthaltenen Funktionen und Schritte zum aufbau der  
Kommunikation mit dem Broker werden hier in einzelnen Codeabschnitten erklärt. 
***
Als erstes Müssen einige Imports aus der hinzugefügten jar gemacht werden. 
```
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.io.Serializable;
import org.eclipse.paho.client.mqttv3.*;
```
***
Danach werden die Variablen für den Mqtt Client und die Mqtt Message wie folgt bekannt gemacht. 
```
private MqttClient client;
private MqttMessage message;
```
sind die Variablen bekannt, wird ein neuer Client erstellt
und die Borker Ip und den Benutzernamen
> #### !!! Wichtig !!!
> Der Benutzernamen innerhalb des ganzen Mqtt darf nirgendwo gleich sein. Auch unter 3 Robotinos nicht
> bei der Auswahl des Nutzernamens muss mit der RobotNr aus dem cfg file gearbeitet werden oder einer 
> immer andere Nummer oder Name
  
```
client = new MqttClient(BorkerIp, ClientId);
```
ist der Client erstellt, wird verbindung mit dem Broker hergestellt mit 
```
client.connect();
```
Danach ist es abhängig davon was gesendet wird. Es können Objekte oder auch nur Strings gesendet werden. 

### <a name="sobj">Objekte Senden</a>
mit dem untenstehenden Code Können ganze Objekte über den Broker gesendet werden. 
der Nachteil daran ist, dass nichts was gesendet wird für den Menschen lesbar ist. 
```
ObjectOutputStream o = null;
        try
        {
            ByteArrayOutputStream b = new ByteArrayOutputStream();
            o = new ObjectOutputStream(b);
            o.writeObject(obj);
            message.setPayload(b.toByteArray());
            client.publish(topic, message);       //blockieren auf setTimeToWait
        } catch (IOException ex)
        {
            System.out.println(ex);
        } finally
        {
            try
            {
                o.close();
            } catch (IOException ex)
            {
            }
        }
```
für das senden ausschlaggebend ist der Topic als String und die Message als beliebiges Objekt mit implements Serzalizable(hier obj). 


### <a name="sst">Strings Senden</a>
Das Senden eines Strings ist wesentlich einfacher.
```
message.setPayload(msg.getBytes());
client.publish(topic, message);
```
für das senden ausschlaggebend ist hier einzig die Nachricht als String (hier msg)
und den Topic ebenfalls als String. 

Wird eine Nachricht Retained gesendet, wird sie auf dem Broker gespeichert und bei jedem anmelden
erneut bei den Teilnemer gesendet(retained = boolean). 
```
message.setRetained(retained);
```