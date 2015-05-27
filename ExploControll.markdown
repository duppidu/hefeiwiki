Diese Klasse handelt die Explorations-Phase des Spiels. Aufgerufen wird die Klasse von der State Machine. Ein Threading der Klasse ist nicht nötig, da die Aktionen der Klasse auf Aktionen auf dem Mqtt-Brocker ausgeführt werden. 

### Konstruktor
Sobald die Klasse instantiiert wird, öffnet sie eine Kommunikation mit dem Mqtt-Brocker und hört auf die Topics auf denen Subscribed wurde (mqtt.setCallback( Reciever , Topic )).


----------


### messageArrived(String topic, MqttMessage message)
wird durch implements MqttCallback erzwungen

Diese Methode wird immer dann aufgerufen, wenn eine nachricht auf einem der Subscribten Topics publiziert wird. und die Methode erhält den Topic und die Nachricht als Übergabewert. Somit kann bei der nachricht auf das entsprechende Topic geprüft werden.  

----------