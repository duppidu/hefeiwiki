[Home](home)  
[Back](DokuSolidus)
***
## Diagramme
### Laserscanner
#### Klassendiagramm
![Laserscanner](https://gitlab.com/solidus/hefei/uploads/a3d0d268ecf3d39f39aa0ddc3f01d902/Laserscanner.png)  
#### Ablaufdiagramm
![Laserscanner_Ablauf](https://gitlab.com/solidus/hefei/uploads/00b8fe26875b2e4a084bae1cf7fc7f1d/Laserscanner_Ablauf.JPG)
***

### StateMachine
#### Setup

![StateMachine_Setup](https://gitlab.com/solidus/hefei/uploads/6e1fc296532cac8615b6257dc3871d31/StateMachine_Setup.JPG)

#### Exploration

![StateMachine_Explo](https://gitlab.com/solidus/hefei/uploads/2137fd10fdde42ed07aa12abb1eecbff/StateMachine_Explo.JPG)

#### Production

Noch nicht fertig entwickelt...
***
### Refbox
Während des Cups gab es bei der ComRefBox Klasse die meisten Änderungen. Aus der ersten Version vor dem Cup und den Änderungen gab es eine zweite Version, welche für eine Explorationsphase funktioniert. Daraus entstanden ein neues Anwendungsfalldiagramm und ein neues Klassendiagramm. 
#### Anwendungsfalldiagramm der ComRefBox 
![Refbox_Anwendungsfalldiagramm_V2](https://gitlab.com/solidus/hefei/uploads/a538db431e478e429c532aad416e0119/Refbox_Anwendungsfalldiagramm_V2.jpg)

Die ganze ExploControl wurde vor dem Cup noch umgekrempelt, dass die Jobs zentral verwaltet werden. Deshalb werden die Explorationsinformationen nicht mehr über den Broker an die ExploControl, sondern an die ExploControlMain gesendet. Die Informationen über entdeckte Maschinen kamen vorher auch vom ExploControl. Neu kommen die Informationen vom ExploControlLocal. Das Registrieren der Nachricht RobotInfo ist im Programm noch vorhanden, wurde aber aus dem Diagramm gelöscht. Im Programm ist die Registratur entsprechend gekennzeichnet.
#### Klassendiagramm der ComRefBox
![Refbox_Klassendiagramm_V2](https://gitlab.com/solidus/hefei/uploads/74adbc0e7781ca4a30cdae274d180bbe/Refbox_Klassendiagramm_V2.jpg)

Einige neue Variablen sind dazugekommen. Die innere Klasse SendBeacon ist nicht mehr in Verwendung und wurde als "deprecated" gekennzeichnet. Das Beaconsignal wird neu in der run-Methode versendet. Die Zonen werden neu von der ExploControlMain im Package Master verarbeitet. Die entdeckten Maschinen werden neu über die ExploControlLocal im Package fieldcommander empfangen. Für diese Kommunikation wurde für die ComRefBox eigens ein neues Topic geschaffen. Die Informationen in der Produktionsphase werden neu im ProductControlMain im Package Master verarbeitet. Die Methode sendMachines wird nicht mehr in der Methode messageArrived, sondern in der run-Methode aufgerufen. Der Maschinenberichteintrag, der Maschinenbericht und die Nachricht selber werden immer noch in der Methode sendMachines aufgebaut. Die Nachricht wird aber neu in der run-Methode verschickt. 
