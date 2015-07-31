[Home](home) [Back](WikiSolidus)

MQTT Topic List
===================


Aufbau MQTT Topic
-------------

/robo/local/...		>	und folgende steht für lokal auf dem Robotino

/field/... 		>	und folgende steht für das Gesamte Spielfeld


Local Topics
-------------

| Was| Sender | Empfänger | Topic | 
| :-------  |:------ |:------ | ----: |
| Nächste Position | Explocontrol / Produktioncontroll | WayController |/robo/local/pos/target | 
| In Position| WayController | Explocontrol / Produktioncontroll |/robo/local/pos/inpos|
| Aktuelle Position | Positioncontroller | Drive | /robo/local/pos/actual   | 
| Input Position | WayController | Explocontrol | /robo/local/pos/input    |  
| Output Position | WayController | Explocontrol | /robo/local/pos/output    | 
| Start Exploring | ? | ? | /robo/local/pos/explore    | 
| Aktuelle Geschwindigkeit | Positioncontroller | WayAnalyzer | /robo/local/pos/speed    |
| Aktionen Für das Drive | Explocontrol / Produktioncontroll / StateMachine | WayController | /robo/local/pos/actions    |  
| Durch Refbox gemeldete Zonen  | ? | ? | /robo/local/refbox/zones    | 
| Tag Nummer| ? | ? | /robo/local/cam/tag|
| Lampen Erkennung | ? | ? | /robo/local/cam/color    |
| Status der State Machine | ? | ? | /robo/local/statemachine/state   |
| Ausweichs Geschwindigkeit | WayAnalyzer | Drive |/robo/local/pos/avoidingSpeed |
| Senden von neuem Job an Robi 1 | ? | ? |/robo/local/job/newjob1|
| Senden von neuem Job an Robi 2 | ? | ? |/robo/local/job/newjob2|
| Senden von neuem Job an Robi 3 | ? | ? |/robo/local/job/newjob3|
|Greifer (open/) | ? | ? |/robo/local/grippercontrol|
|Aktuelle Spielphase von Refbox | ? | ? |/robo/local/refbox/phase|
|Aktueller Spielstatus von Refbox | ? | ? |/robo/local/refbox/state|
|Position Initialisiert | StateMachine | WayController |/robo/local/pos/init|
|Robotino Neustarten | ? | ? |/robo/local/restart|


Field Topics
-------------

| Was| Sender | Empfänger | Topic | 
| :-------  |:------ |:------ | ----: |
| Job Anfrage (Production "Robi sendet seine Nummer") | ? | ? |/field/job/getjob|
| Maschinen werden Gesendet um Feld zu vervollständigen | ? | ? |/field/complete/machine|
| Komplette Maschinen Map wird zur Sicherheit gesendet | ? | ? |/field/map/machine|
| Sendet Robotinonummer des Robotinos, welcher bereit auf dem Feld steht | ? | ? |/field/stateMachine/onField|
| Alle Zonen von Refbox als String Bsp: "Z1-Z2-Z3" | ? | ? |/field/refbox/zones|

Schlüsselwörter
-------------
| Topic| Message| Aktion|
| :-------  |:------ |:------ | 
|/robo/local/pos/target | Coord Objekt mit der Zielposition | Der WayController setzt dem Drive das target Attribut.|
|/robo/local/pos/inpos | String "target" | Der Robotino hat beim "goToTarget" Befehl das Ziel erreicht. |
|/robo/local/pos/inpos | String "field" | Der Robotino hat beim "goToField" Befehl das Ziel erreicht. |
|/robo/local/pos/inpos | String "mps" | Der Robotino vor der MPS und ist bereit für die Tagerkennung. |
|/robo/local/pos/inpos | String "belt" | Der Robotino hat die MPS angefahren und steht vor dem Band. |
|/robo/local/pos/inpos | String "belt.1" | Der Robotino hat die MPS angefahren und steht vor der ersten Offsetposition. |
|/robo/local/pos/inpos | String "belt.2" | Der Robotino hat die MPS angefahren und steht vor der zweiten Offsetposition. |
|/robo/local/pos/inpos | String "belt.3" | Der Robotino hat die MPS angefahren und steht vor der dritten Offsetposition. |
|/robo/local/pos/inpos | String "belt.4" | Der Robotino hat die MPS angefahren und steht vor der vierten Offsetposition. |
|/robo/local/pos/inpos | String "backwards" | Der Robotino hat die Gewünschte Distanz zur MPS erreicht und ist bereit für ein neues Ziel.|
|/robo/local/pos/actual | Coord Objekt mit der aktuellen Position | Das actual Attribut im Drive wird überschrieben.|
|/robo/local/pos/input | Coord Objekt mit den berechneten Input Koordinaten. | ? |
|/robo/local/pos/output| Coord Objekt mit den berechneten Output Koordinaten.| ? |
|/robo/local/pos/explore | ? | ?|
|/robo/local/pos/speed | Speed Objekt mit der aktuellen Geschwindigkeit.| Das actualSpeed Attribut im WayAnalyzer wird überschrieben.|
|/robo/local/pos/actions | String "goToTarget" | Der Robotino fährt zum aktuellen Ziel. Sobald das Ziel erreicht wurde wird ein "target" gesendet. |
|/robo/local/pos/actions | String "goToField" | Der Robotino fährt zum aktuellen Ziel. Sobald das Ziel erreicht wurde wird ein "field" gesendet. |
|/robo/local/pos/actions | String "explore" | Der Robotino sucht eine MPS im aktuellen Feld. Sobald sie angefahren wurde wird ein "mps" gesendet.|
|/robo/local/pos/actions | String "stop" | Alle Antriebe des Robotinos werden ausgeschaltet und nach einer gewissen Zeit wieder eingeschaltet.|
|/robo/local/pos/actions | String "pause" | Pausenstatus der Refbox. Alle Antriebe des Robotinos werden ausgeschaltet. |
|/robo/local/pos/actions | String "play" | Pausenstatus der Refbox aufgehoben. Das Drive Programm läuft weiter.|
|/robo/local/pos/actions | String "calcOtherSide" | WayController berechnet die gegenüberliegende Seite der MPS und fährt anschliessend dort hin.|
|/robo/local/pos/actions | String "goToMPS" | Der Robotino fährt zum aktuellen Ziel. Sobald das Ziel erreicht wurde wird ein "mps" gesendet. |
|/robo/local/pos/actions | String "approach" | Der Robotino fährt vor das Band der MPS. Sobald er es erreicht hat wird ein "belt" gesendet.|
|/robo/local/pos/actions | String "approach.1" | Der Robotino fährt an die erste Offsetposition der MPS. Sobald er es erreicht hat wird ein "belt.1" gesendet.|
|/robo/local/pos/actions | String "approach.2" | Der Robotino fährt an die zweite Offsetposition der MPS. Sobald er es erreicht hat wird ein "belt.2" gesendet.|
|/robo/local/pos/actions | String "approach.3" | Der Robotino fährt an die dritte Offsetposition der MPS. Sobald er es erreicht hat wird ein "belt.3" gesendet.|
|/robo/local/pos/actions | String "approach.4" | Der Robotino fährt an die vierte Offsetposition der MPS. Sobald er es erreicht hat wird ein "belt.4" gesendet.|
|/robo/local/pos/actions | String "backwards" | Der Robotino fährt rückwärts bis er die parametrierte Distanz erreicht hat.|
|/robo/local/pos/actions | String "initCoords" | Die Position der Robotinos wird initialisiert.|
|/robo/local/refbox/zones| ? | ?|
|/robo/local/cam/tag| ? | ?|
| /robo/local/statemachine/state | ? | ?|
|/robo/local/pos/avoidingSpeed | Speed Objekt mit der Ausweichgeschwindigkeit| Die Ausweichgeschwindigkeit wird dem Omnidrive weitergegeben.| 
|/robo/local/job/newjob1 | ? | ?| 
|/robo/local/job/newjob2 | ? | ?| 
|/robo/local/job/newjob3 | ? | ?| 
|/robo/local/grippercontrol | ? | ? |
|/robo/local/refbox/phase | ? | ? |
|/robo/local/refbox/state | ? | ? |
|/robo/local/pos/init | ? | ? |
|/robo/local/restart | ? | ? |




