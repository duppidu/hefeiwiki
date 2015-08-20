[Back](wikisolidus)  
[Home](home)  
***
# StateMachine

Die StateMachine ist sozusagen der Chef der Abläufe. Sofern die SubStateHandler nicht selbst den jeweiligen Ablauf handelt, greift die StateMachine ein und verwaltet und steuert die Abläufe. Sie hat engen Kontakt mit der Refbox und hört vorallem auf die gemeldeten Spielphasen.
## Setup
Ursprünglich vorgesehen war, dass in der Setupphase die Position der Robotinos gesetzt wird. Dies wurde aber am Robocup 2015 noch geändert. So handelt die StateMachine jetzt in der Setupphase nichts. Siehe auch: [PositionSet](PositionSet)
## Exploration
![StateMachine](https://gitlab.com/solidus/hefei/uploads/f9e65bbf59dbf77f651af4a76a82c2c5/StateMachine.PNG)
## Production
Die Produktion wurde noch nicht programmiert.
