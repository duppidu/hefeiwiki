### Laserscanner
Aus dem mehrheitlich unkommentierten Code des environmentsensing muss ein grober Überblick geschaffen werden. Die Linien werden bereits [extrahiert](LineExtracter) und gefiltert. Es müssen noch mehr Filter eingefügt werden (nach Zonen, nach Länge). Ein Algorithmus muss programmiert werden, der einen Punkt vor der Maschine errechnet. Ausserdem muss der Punkt vom Laser aus auf das absolute Spielfeld umgerechnet werden.
### StateMachine
Viele Abläufe werden mit eigenen Handlern gesteuert (Exploration: [ExploControll](ExploControll)). Was diese Handler nicht übernehmen, steuert die StateMachine. Sie hat engen Kontakt mit der Refbox und hört direkt auf die Phasen, welche von der Refbox gemeldet werden.
### Refbox