MQTT Topic List
===================


Aufbau MQTT Topic
-------------

/robo/local/...		>	und folgende steht für lokal auf dem Robotino

/robo/master/... 		>	und folgende steht für das Gesamte Spielfeld


Local Topics
-------------

| What   | Topic | 
| :------- | ----: |
| Nächste Position |/robo/local/pos/target | 
| In Position|/robo/local/pos/inpos|
| Aktuelle Position | /robo/local/pos/actual   | 
| Input Position | /robo/local/pos/input    |  
| Output Position | /robo/local/pos/output    | 
| Start Exploring | /robo/local/pos/explore    | 
| Aktuelle Geschwindigkeit | /robo/local/pos/speed    |
| Aktionen Für das Drive | /robo/local/pos/actions    |  
| Durch Refbox gemeldete Zonen  | /robo/local/refbox/zones    | 
| Pause| /robo/local/refbox/pause    | 
| Tag Nummer| /robo/local/cam/tag|
| Lampen Erkennung| /robo/local/cam/color    |
| Status der State Machine| /robo/local/statemachine/state   |
| Ausweichs Geschwindigkeit +/- |/robo/local/pos/avoidingSpeed |


Field Topics
-------------

| What   | Topic | 
| :------- | ----: |
| comes | later |