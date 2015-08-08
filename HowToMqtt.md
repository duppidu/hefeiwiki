[Home](home) [Back](WikiSolidus)

# Inhalt  

- <a name="RecMsg">Nachrichten Empfangen</a>
- <a name="msgArr">MessageArrived(String topic, MqttMessage message) </a>
-- <a name="RecObj">Objekte Empfangen</a>
-- <a name="RecSt">String Empfangen</a>
- <a name="connLost">connectionLost(Throwable thrwbl)</a>
- <a name="delcomp">deliveryComplete(IMqttDeliveryToken imdt)</a>
- <a name="usrEx">Benutzerbeispiel</a>

### <a name="RecMsg">Nachrichten Empfangen</a>
Um in einer Klasse eine Nachricht zu empfangen, egal ob Objekt oder String, müssen
zuerst 4 Dinge gemacht werden.
1. Als erstes müssen die Nötigen Imports gemacht werden. 
2. In der Klasse muss "implements MqttCallback" hinzugefügt werden.  
3. Es muss eine neue MqttCom instanziert werden. Die Methode hatt die IP des Broker's und den Benutzernamen als Übergabewert
4. Es muss ein Callback auf alle benötigten Topics gemacht werden. Die Methode hatt den Empfänger und den entsprechenden Topic als Übergabewert.
```
import org.eclipse.paho.client.mqttv3.IMqttDeliveryToken;
import org.eclipse.paho.client.mqttv3.MqttCallback;
import org.eclipse.paho.client.mqttv3.MqttException;
import org.eclipse.paho.client.mqttv3.MqttMessage;
```

```
implements MqttCallback
```

Mit dem implements MqttCallback werden 3 Methoden erzwungen.

- messageArrived(String topic, MqttMessage message)
-- wird immer dann aufgerufen, wenn auf einem subscribten Topic eine Nachricht ankommt
- connectionLost(Throwable thrwbl)
-- wird aufgerufen sobald die verbindung zum Mqtt server unerwartet verloren geht
- deliveryComplete(IMqttDeliveryToken imdt)
-- wird nach jedem erfolgreichen senden aufgerufen

```
mqtt = new MqttCom("tcp://192.168.1.2:1883", "MqttUserName");
```
Mit dieser Instanzierung Wird eine neue Kommunikation zum Broker aufgebaut. 
> Wichtig!!!
> Global darf nicht 2 mal der Selbe Usernamen existieren also muss jede Klasse auf jedem Robotino einen anderen Namen tragen

```
mqtt.setCallback(this, PathInPos);
```
Mit dem setCallback wird erreicht, dass bei jeder nachricht auf dem angegebenen Topic die MessageArrived Methode aufgerufen wird. Der erste Übergabewert in der Klammer, beschreibt den Empfänger und der Zweite Ist der String mit dem Topic

### <a name="msgArr">MessageArrived(String topic, MqttMessage message) </a>
Diese Methode wird immer dann aufgerufen, wenn auf einem Subscribten Topic eine Nachricht gesendet wird.
der Methode werden bei jeder Nachricht der entsprechende Topic und die Nachricht selber übergeben. 
mit einem Case im MessageArrived kann sehr effizient auf die Topics geprüft werden und ensprechend reagiert werden.   

> #### Wichtig !!
> In der MessageArrived Methode können weder Sendeaktionen mit dem MQTT noch grosse Methoden aufgerufen werden. Desshalb wird vielfach in Verbindung mit der MqttCom auch ein scheduliertes Run verwendet und mit booleans als bindeglied gearbeitet. 
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

### <a name="usrEx">MQTT COM Benutzerbeispiel</a>
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
