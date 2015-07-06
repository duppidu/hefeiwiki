[Home](home) [Back](WikiSolidus)

MQTT Topic List
===================


Aufbau MQTT Topic
-------------

/robo/local/...		>	und folgende steht für lokal auf dem Robotino

/field/... 		>	und folgende steht für das Gesamte Spielfeld


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
| Senden von neuem Job an Robi 1 |/robo/local/job/newjob1|
| Senden von neuem Job an Robi 2 |/robo/local/job/newjob2|
| Senden von neuem Job an Robi 3 |/robo/local/job/newjob3|
|Greifer (open/)|/robo/local/grippercontrol|
|Aktuelle Spielphase von Refbox|/robo/local/refbox/state|
|Position Initialisiert|/robo/local/pos/init|
|Robotino Neustarten|/robo/local/restart|


Field Topics
-------------

| What   | Topic | 
| :------- | ----: |
| Job Anfrage (Production "Robi sendet seine Nummer") |/field/job/getjob|
| Maschinen werden Gesendet um Feld zu vervollständigen|/field/complete/machine|
| Komplette Maschinen Map wird zur Sicherheit gesendet|/field/map/machine|
| Sendet Robotinonummer des Robotinos, welcher bereit auf dem Feld steht|/field/stateMachine/onField|