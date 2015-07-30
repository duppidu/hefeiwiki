[Home](home) [Back](WikiSolidus)

# Inhalt  
- <a href="#lib">Library</a>
- <a href="#com">MQTT COM</a>
- <a href="#sobj">Send Objects</a>
- <a href="#sst">Send String</a>
- <a name="RecMsg">Nachrichten Empfangen</a>
- <a name="msgArr">MessageArrived(String topic, MqttMessage message) </a>
-- <a name="RecObj">Objekte Empfangen</a>
-- <a name="RecSt">String Empfangen</a>
- <a name="connLost">connectionLost(Throwable thrwbl)</a>
- <a name="delcomp">deliveryComplete(IMqttDeliveryToken imdt)</a>


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
### <a name="RecMsg">Nachrichten Empfangen(nicht in MqttCom)</a>
Um in einer Klasse eine Nachricht zu empfangen, egal ob Objekt oder String, müssen
zuerst 3 Dinge gemacht werden.
In der Klasse muss "implements MqttCallback" hinzugefügt werden und die untenstehenden Codezeilen
```
        client.subscribe(topic);
        client.setCallback(receiver);
```
mit dem client.subscribe(topic) empfängt mann jede nachricht von entsprechenden Topic
und mit dem client.setCallback(reciever) wird bestimmt wer die Nachrichten erhält also in den meisten fällen this für die eigene Klasse.   
Mit dem implements MqttCallback werden 3 Methoden erzwungen.

>- messageArrived(String topic, MqttMessage message)  
>-- wird immer dann aufgerufen, wenn auf einem subscribten Topic eine Nachricht ankommt  
>- connectionLost(Throwable thrwbl)  
>-- wird aufgerufen sobald die verbindung zum Mqtt server unerwartet verloren geht  
>- deliveryComplete(IMqttDeliveryToken imdt)  
>-- wird nach jedem erfolgreichen senden aufgerufen  

### <a name="msgArr">MessageArrived(String topic, MqttMessage message) </a>
Diese Methode wird immer dann aufgerufen, wenn auf einem Subscribten Topic eine Nachricht gesendet wird.
der Methode werden bei jeder Nachricht der entsprechende Topic und die Nachricht selber übergeben. 
mit einem Case im MessageArrived kann sehr effizient auf die Topics geprüft werden und ensprechend reagiert werden.   

> #### Wichtig !!
> In der MessageArrived Methode können weder Sendeaktionen mit dem MQTT noch grosse Methoden aufgerufen werden. Desshalb wird vielfach in Verbindung > mit der MqttCom auch ein scheduliertes Run verwendet und mit booleans als bindeglied gearbeitet. 
> 
  
#### <a name="RecObj">Objekte Empfangen</a>
Ist im MessageArrived das empfangen von Objekten nötig, werden folgende Codezeilen benötigt
```
ByteArrayInputStream b = new ByteArrayInputStream(message.getPayload());
```
der ByteArrayInputStream kann auch nur 1 mal pro MessageArrived aufgerufen werden. Eventuell könnten auch die 2 Zeilen im nächsten abschnitt nur 1 mal aufgerufen werden, wir haben es jedoch nie getestet. 
```
ObjectInputStream o = new ObjectInputStream(b);
Serializable d = (Serializable) o.readObject();
lamps = (Lamps) d;
```
Wichtig ist, dass die Objekte welche gesendet werden je Topic genau definiert sind. Ist das nicht der Fall, kommt es bei der Lezten Zeile im Oberen abschnitt bei der Castingoperation zu einem Fehler. 
ist das Objekt lamps welches wir vom Broker erhalten haben erst mal gespeichert, wird bei jeder Message arrived wider überschrieben. 

#### <a name="RecSt">String Empfangen</a>
Ein String zu empfangen ist wesentlich einfacher. Es empfielt sich jedoch auch hier mit einem Case zu arbeiten.
```
message.toString(); //Reicht um ein String auszugeben
if (message.toString().equals("backwards")) //Message auf String prüfen
{
	//Some Code 
}
```
Die Message kann in einem if oder einem Case geprüft werden das spielt keine Rolle.

### <a name="connLost">connectionLost(Throwable thrwbl)</a>
Standartmässig wird bei dieser Methode eine Codezeile hinzugefügt.
```
throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
```
diese Zeile wirft eine Exception sobald die Methode aufgerufen wird. Um hänger im Programm zu vermeiden
ist es empfehlenswert statt dessen ein SystemOut einzutragen oder besser ein Loggereintrag.

### <a name="delcomp">deliveryComplete(IMqttDeliveryToken imdt)</a>
Standartmässig wird auch bei dieser Methode eine Codezeile hinzugefügt.
```
throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
```
diese Zeile wirft eine Exception sobald die Methode aufgerufen wird. Hier ist es erst recht empfehlenswert statt der Exception ein SystemOut einzutragen, ein Loggereintrag oder die Zeile einfach auskommentieren. Denn die Methode wird nach jedem erfolgreichen Senden aufgerufen. 

### <a name="delcomp">MQTT COM Benutzerbeispiel</a>
Folgender Code ist in Teilen aus der ExploControllLocal Kopiert

```
import org.eclipse.paho.client.mqttv3.IMqttDeliveryToken;
import org.eclipse.paho.client.mqttv3.MqttCallback;
import org.eclipse.paho.client.mqttv3.MqttException;
import org.eclipse.paho.client.mqttv3.MqttMessage;

public class ExploController implements MqttCallback, Runnable
{
    /**
     * ExploControll Class Lisents to different Topics on a MQTT Brocker each
     * time a message arrives messageArrived(String topic, MqttMessage message)
     * gets Callet with if (topic.equals("Topic")) you can check on witch topic
     * the Message arrived.
     *
     * then the different Messages ar followed by different Actions
     *
     */
    public ExploController() throws MqttException
    {
        mqtt = new MqttCom("tcp://" + StartUp.cfg.robotIp + ":1883", PathMqttUser);
        mq = new MqttCom("tcp://" + StartUp.cfg.mqttBrokerIp + ":1883", PathMqttUser);
        
        try
        {
            /**
             * Mit dem x.setCallback wird definiert, wer welchen  Topics zuhört.
             * Das This in der Klammer definiert, wer die Nachrichten erhält.
             * Der hintere String definiert auf das zu hörende Topic.
             */

            mqtt.setCallback(this, PathInPos);
            mqtt.setCallback(this, PathRefbox);
            mqtt.setCallback(this, PathNewTarget);
            mqtt.setCallback(this, PathTag);
            mqtt.setCallback(this, PathColor);
            mqtt.setCallback(this, PathPosIn);
            mqtt.setCallback(this, PathPosOut);
            mqtt.setCallback(this, PathActions);
            mq.setCallback(this, PathMachine);

        } catch (MqttException ex)
        {
            //Gibt allfällige exceptions aus.
            ExploLog.error("Callback Exception", ex);
        }
        //Scheduler im allgemeinen Pool starten.
        StartUp.exSrv.scheduleAtFixedRate(this, 0, 200, TimeUnit.MILLISECONDS);

    }

    /**
     * In dieser Klasse mussten wir eine Run Methode einfügen, weil aus der
     * Methode messageArrived() nicht gesendet werden kann. Wird es doch gemacht,
     * fällt die gesammte Klasse in einen Error, welcher nur durch einen Neustart
     * behoben werden kann.
     */
    @Override
    public void run()
    {
        if (sendRefb)
        {
            try
            {
                mqtt.send(PathNewTarget, jobHandler());
                mqtt.sendString(PathActions, "goToField");
                sendRefb = false;
            } catch (MqttException ex)
            {
                ExploLog.error("MQTT Exception Neues Feld Senden", ex);
            }
        }
    }

    /**
     * Diese Methode wird immer aufgerufen, wenn auf einem x.setCallback
     * subscribten Topic eine Nachricht gesendet wird. Bei dem Aufruf wird immer
     * der entsprechende Topic Name und die Nachricht übergeben.
     *
     * @param topic -Topic on witch the message is transmitted
     * @param message -Message Transmitted on the Broker
     * @throws Exception -MQTT Error
     */
    @Override
    public void messageArrived(String topic, MqttMessage message) throws Exception
    {
        ByteArrayInputStream b = new ByteArrayInputStream(message.getPayload());

        /**
         * Wird auf dem Topic PathInPos backwards gesendet, so wird die Boolean
         * sendRefb auf true gesetzt. Damit wird das nächste Ziel gesendet.
         *
         */
        if (topic.equals(PathInPos))
        {

            if (message.toString().equals("backwards"))
            {
                
                sendRefb = true;
            }
            if (message.toString().equals("next"))
            {
              
                sendRefb = true;
            }

        }
        /**
         * IF Message Arrived from PathColor wird die erkannte Lampe mit ihren
         * zuständen gespeichert. Um die Maschine zu ergänzen.
         */
        if (topic.equals(PathColor))
        {
            try
            {
                ObjectInputStream o = new ObjectInputStream(b);
                Serializable d = (Serializable) o.readObject();
                lamps = (Lamps) d;
                ExploLog.debug("Lamp Recieved: "+lamps.toString());

            } catch (IOException | ClassNotFoundException ex)
            {
                System.out.println(ex);

            }
        }   
    }

    /**
     * Von dem Interface MqttCallback erzwungene Methode.
     *
     * @param thrwbl
     */
    @Override
    public void connectionLost(Throwable thrwbl)
    {
        ExploLog.error("MQTT Connection Lost"); // creates Log Entry
    }

    /**
     * Vom Interface MqttCallback erzwungene Methode
     *
     * @param imdt
     */
    @Override
    public void deliveryComplete(IMqttDeliveryToken imdt)
    {
        //throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
}
```
***
