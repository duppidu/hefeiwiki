[Home](home)  
[Back](KonzeptMFT)  
### Laserscanner
Aus dem mehrheitlich unkommentierten Code des environmentsensing muss ein grober Überblick geschaffen werden. Die Linien werden bereits [extrahiert](LineExtraction) und gefiltert. Es müssen noch mehr Filter eingefügt werden (nach Zonen, nach Länge). Ein Algorithmus muss programmiert werden, der einen Punkt vor der Maschine errechnet. Ausserdem muss der Punkt vom Laser aus auf das absolute Spielfeld umgerechnet werden.  
Ausserdem ist es bequem, wenn der Laser bereits in der ersten Messecke erkennt, dass sich keine Maschine im Feld befindet und so weiterfährt.
### StateMachine
Viele Abläufe werden mit eigenen Handlern gesteuert (Exploration: [ExploControll](ExploControll)). Was diese Handler nicht übernehmen, steuert die StateMachine. Sie hat engen Kontakt mit der Refbox und hört direkt auf die Phasen, welche von der Refbox gemeldet werden. Die StateMachine hat höhere Priorität.  
Sie kommuniziert auschliesslich über den Broker mit den anderen Klassen.
### PositionSet
Die Positionssetzung am Anfang des Spieles soll vollständig automatisch erfolgen. Dazu müssen jedoch vor dem ersten Spiel die korrekten Banden ausgemessen und in den Code eingetragen werden. Ausserdem liest das Programm die Spielfarbe und -seite automatisch aus und passt so die Positionen an.
### Refbox
Die Refbox kann wahlweise auf einem Fedora oder auf einem Ubuntu-System installiert werden. Dazu gibt es gute Anleitungen vom Programmierer im Internet. Da das Ubuntu-System einfacher zu handhaben ist, wollten wir die Refbox auf einem Ubuntu Trusty Thar installieren. Bei der Installation nach der Anleitung trat leider immer der gleiche Fehler auf. Anscheinend ein Softwarefehler. Deshalb wechselten wir auf Fedora 21. Das System mit der Refbox wird auf einer virtuellen Maschine laufen, so dass das System weitergegeben werden kann. Für dieses Vorhaben steht Oracles VM Virtualbox Manager zur Verfügung. Mit dieser Software kann jedes System simuliert werden. Dazu wird nur eine ISO des System zur Installation benötigt. 
### RobotinoOS
Für die Aktualisierung der Robotino-Firmware gibt es auf dem Robotinowiki eine gute Anleitung. Für die weiteren Softwareteile, z. B. Java, werden die Anleitungen im Internet gesucht und die wichtigsten Schritte werden dokumentiert. Da die Firmware auf Ubuntu basiert, können viele Informationen gefunden werden. Bereits das [Ubuntuusers Wiki](https://wiki.ubuntuusers.de/Startseite) beinhaltet sehr viele und hilfreiche Informationen und Anleitungen über die verschiedenen Facetten des Linux-Systems Ubuntu.   
Für die Images hat sich PartImage empfohlen. Die Software wird im Internet einige Male empfohlen und es gibt einige Anleitungen dazu. Sie ist ein Teil der SystemRescueCD. Die SystemRescueCD kann auf einfache Weise auf einen USB-Stick gebracht werden und besitzt eine grafische Oberfläche. 