[Home](home)  
[Back](KonzeptMF)  
## RefBox
![Schnittstellen](https://gitlab.com/solidus/hefei/uploads/4a7cd0b9b5cf1010b0687d039165404a/Schnittstellen.png)

## Laserscanner
Die einzigen Schnittstellen des Laserscanners sind im [Wayanalyzer](Wayanalyzer), im [Waycontroller](Waycontroller) und im [Drive](Drive). Da der Laserscanner Singleton gemacht wird, kann der Laserscanner überall dort aufgerufen werden, wo er gebraucht wird.

## StateMachine

Die StateMachine kommuniziert ausschliesslich mit dem Broker. Auf verschiedenen Topics werden Messages empfangen. Auf anderen werden Befehle gesendet. Zu genaueren Informationen zu den Topics: 