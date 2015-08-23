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
![Refbox_Anwendungsfalldiagramm_V1](https://gitlab.com/solidus/hefei/uploads/57bdf3f642fb479c66a1269bfdef09f4/Refbox_Anwendungsfalldiagramm_V1.jpg)

Beim Anwendungsfalldiagramm hat sich seit dem Prozessmodul nichts mehr geändert. 
In der Mitte steht die Klasse mit allen Nachrichten, welche verschickt oder empfangen werden. Zudem steht darunter immer über welchen Kanal die Nachrichten laufen. Ausserhalb ist die Refbox, welche ihrerseits die Nachrichten versendet oder empfängt. Sowie die anderen Klassen mit denen eine Kommunikation stattfindet. Die Pfeile geben an in welche Richtung die Informationen geschickt respektive empfangen werden. Die alleinstehende Nachricht RobotInfo wird im alten Code als Nachricht definiert. Laut dem Refbox Manual ist die Nachricht aber nicht für Roboter bestimmt. 

![Refbox_Klassendiagramm_V1](https://gitlab.com/solidus/hefei/uploads/655ea15ee7715d31bca523b5423eebe3/Refbox_Klassendiagramm_V1.jpg)

Bei der Prozessmodul Dokumentation ist das Klassendiagramm noch nicht vollständig. 
Das ist nun das konzeptionelle Klassendiagramm. Die meisten Variablen und die zwei inneren Klassen "Handler" und "SendBeacon" werden vom letztjährigen Code übernommen. Neu wird für jede Nachricht eine eigene Methode geschrieben. Dadurch wird im Handler bei der Ankunft einer Nachricht nur noch die entsprechende Methode aufgerufen. Zusätzlich wird die Brokerkommunikation neu eingebaut. Ist ein ausgefüllter Pfeil (Assoziation) dargestellt, ist der Zugriff nicht zwingend direkt auf eine Klasse oder auf ein Objekt. Sondern es kann auch eine Kommunikation mittels dem Broker darstellen. Im Manual der Refbox ist eine Veröffentlichung der Koordinaten der Roboter empfohlen. Deshalb ist eine Assoziation zur Klasse Coord dargestellt. Diese Funktion wird nicht unbedingt benötigt und wird nur programmiert, wenn genügend Zeit vorhanden ist. Diese Idee könnte aber gut weiterverfolgt werden. Mit JavaFX könnte eine grafische Oberfläche gestaltet werden, auf dem ersichtlich ist, wo sich die Roboter auf dem Spielfeld aufhalten. Daraus ergäben sich viele weitere Vorteile. Das Vorstellen des Projektes könnte so interessanter gestaltet werden, Fehler könnten schneller gefunden werden und die aktuellen Arbeiten eines Roboters können übersichtlicher und einfacher überwacht werden. 

### ColorDetection  
Die ColorDetection soll mit hilfe der OpenCV Bibliothek das erkennen der Lamoensäule übernehmen. OpenCV ist eine Bibliothek die viele Methoden im bereich der Bildauswertung beinhaltet. Das Programm soll erkennen welche der Lampen eingeschalten ist und welche ausgeschalten. Das Detektierte Farbbild soll dann in ein Lampen Objekt gespeichert werden und dieses soll dann auf den Broker gesendet werden.  
Die Position der Lampe kann über OpenCV eingeschränkt werden so kann sicher gegangen werden das man nur die Lampensäule detektiert und nicht andere Leuchtende Dinge.

