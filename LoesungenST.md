[Home](home)   
[Back](DokuSolidus)    

----------

## Thomas

Die Kommunikation mit dem Broker wurde über einen MQTT-Client gelöst. Mit diesem ist es möglich Elemente zu senden. Zusätzlich musste in der ColorDetection Klasse noch die Implementation eines MqttCallback gemacht werden, durch diese können nun auch Meldungen die vom Broker auf das eingeschriebene Topic gesendet werden ausgewertet werden.  
Um die Vollständige Kommunikation mit senden und empfangen zu realisieren mussten folgende Schritte befolgt werden:
- erst muss auf den Broker connectet werden  
- danach muss sich auf das Topic eingeschrieben werden (subscribe)  
- als letztes muss noch das Callback auf die gleiche Klasse gesetzt werden (this)

