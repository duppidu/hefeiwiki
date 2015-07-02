[Home](home)   
[Back](DokuSolidus)    

----------

## Thomas

Die Kommunikation mit dem Broker wurde über einen MQTT-Client gelöst. Mit diesem ist es möglich Elemente zu senden. Zusätzlich musste in der ColorDetection Klasse noch die Implementation eines MqttCallback gemacht werden, durch diese können nun auch Meldungen die vom Broker auf das eingeschriebene Topic gesendet werden ausgewertet werden.  
Um die Vollständige Kommunikation mit senden und empfangen zu realisieren mussten folgende Schritte befolgt werden:
- erst muss auf den Broker connectet werden  
- danach muss sich auf das Topic eingeschrieben werden (subscribe)  
- als letztes muss noch das Callback auf die gleiche Klasse gesetzt werden (this)


##  Simon

###  MarkerCoordinates:

Damit wir die ALVAR Bibliothek verwenden können obwohl wir nur Java verwenden, benutzte ich JNA (JavaNativeAccess). Das geschriebene Javaprogramm ruft generiert also einen neuen Prozess, in welchem das C++ Programm läuft. Dieses prüft nun das Kamerabild auf einen Marker und gibt seine Position als return Wert zurück. Aufgrund des Umstandes, dass dieser Wert in Pixel angegeben wird, kann man die Position des Markers sehr genau bestimmen. Mit diesem Wert arbeitet nun Bryans Drive Klasse weiter und kann so den Robotino anhand des Markers ausrichten. 


###  ServoControl:

Die Steuerung der Servos wird über ein ServoBrick von thinkerforge erledigt. Dieser ist über USB am Robotino angeschlossen. Das Javaprogramm steuert also diesen Servobrick an. Im Programm können diverse Parameter für die Servosteuerung gesetzt werden wie zum Beispiel Beschleunigung öffnen/schliessen, Geschwindigkeit öffnen/schliessen usw. . Anschliessend wird über einen MQTT-Callback ein Topic des MQTT Brokers überprüft auf die Inputs "open" oder "close". Je nach Input verfahren die Servos in eine definierte "open-position" oder "close-position". 
