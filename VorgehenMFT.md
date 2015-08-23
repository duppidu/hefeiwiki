[Home](home)  
[Back](DokuSolidus)
***
### Quellen: 
[Symbol von Robotino](http://www.festo-didactic.com/ov3/media/customers/1100/robotinotopview_2.png)

***
## ColorDetection

### Device Problem
Es wurde festgestellt das ein Problem mit der Device - Wahl vom C++ Teil der Markerdedektierung bestand. Das C++ Programm gab immer einen Fehler zurück wenn die Kamera der Colordetection an war.   
Um das Device Problem zu lösen wurde eine Möglichkeit gesucht die Kamera abzuschalten. Nach langem probieren dies über Java zu lösen wurde festgestellt das ein Problem mit der aktuellen OpenCV Version besteht da auch durch null setzen der ganzen Methode wurde die Kamera nicht abgeschaltet.
Lief das Programm in einem separaten Prozess stellte die Kamera ohne Fehler wie gewünscht ab. Also wurde nach einer Lösung gesucht wie man einen separaten Prozess für diese Methode erstellen konnte.   
Es wurde dann Lösung gefunden einen neuen Prozess über ein separates .jar - File zu starten.  

### Blinklichterkennung

Das Blinken der Lampe muss für die Explorationsphase nicht erkannt werden und in der Produktionsphase kann man durch abfrage bei der Refbox den Zustand der Maschine erhalten somit kann auch da auf die auswertung der Lampe verzichtet werden. Aus diesem Grund soll das Erkennen von Blinken auskommentiert werden. Falls aber in einem anderen Jahr Blinken nun doch erkannt werden muss soll dieser Programm abschnitt noch vorhanden sein. 

### Ernneute Überprüfung bei Fehlerkennung

Während des Cups kam es immer wider vor das die Farbdedektierung für alle 3 Lampen False zurückgegeben hatte und dies ist ein im Spiel nicht möglicher Zustand. Dies lag daran das der Bereich der Lampensäule nicht mehr in der Toleranz des Programmes lag. Also entschieden wir uns das wenn dieser Fall eintrift der Suchbereich erst nach Links und falls dies nochmal eintrifft nach rechts verschoben wird.

## ComRefBox
Die Klasse funktionierte bereits mit der diesjährigen Refbox. Einige Nachrichten der Refbox und das Aussehen der Shell haben sich seit dem letzten Jahr geändert. Die meisten Nachrichten sind aber gleich geblieben. Zuerst musste ich mich in die Änderungen gegenüber dem letzten Jahr einlesen. Dafür habe ich das Manual von 2014 gelesen und übersetzt. Das Manual von 2015 war zu dieser Zeit leider noch nicht verfügbar. Das war schon das letzte Jahr ein Problem. Letztes Jahr hatten sie auch diese Klasse erst direkt am Cup programmiert. 

Vor der Programmierung musste die aktuellste API heruntergeladen und im Projekt als .jar-File hinzugefügt werden. Zudem müssen die neuen Nachrichten als .proto-Files in Java-Dateien kompiliert und im Projekt eingefügt werden. Sobald die neuen Nachrichten eingefügt waren, zeigten sich die Änderungen, indem Fehler im Code auftraten. Die Fehler wurden korrigiert und dann noch einmal getestet, ob die Kommunikation noch funktioniert. Dieser Test verlief erfolgreich. Die Klasse war nicht mehr ganz aktuell und war sehr unübersichtlich. Deshalb wurde entschieden für jede Nachricht eine eigene Methode zu programmieren. Mit einem Anwendungsfalldiagramm wurden die Beziehungen dargestellt. 

![Refbox_Anwendungsfalldiagramm_V2](https://gitlab.com/solidus/hefei/uploads/5b6196f1893c4a5cb4434186ea60a427/Refbox_Anwendungsfalldiagramm_V2.jpg)

Darauf ist dargestellt, welche Nachrichten von der Refbox für den Roboter relevant sind und in welche Richtung sie gesendet werden. Zudem ist darauf zu sehen, mit welchen anderen Klassen die ComRefBox kommuniziert. Das Diagramm half, um den ersten Schritt für die Umsetzung zu machen. Vieles musste nur umstrukturiert oder auch unbenannt werden. Einzig die Methode zum Verarbeiten der Explorationsnachricht und die Methode zum Senden der entdeckten Maschinen musste von Grund auf neu programmiert werden. Zudem kam zusätzlich zu letztem Jahr der Broker hinzu. Er dient als zentrale Schnittstelle, um Nachrichten zwischen den Klassen auszutauschen und zu verteilen. 

Die StateMachine benötigt die aktuelle Spielphase und den Spielstatus, um den ganzen Programmablauf vom Roboter zu dirigieren. Der ExploController benötigt die ankommenden Zonen, um den Explorationsweg zu planen. Der ProductController benötigt die Informationen, welche in der Produktionsphase ankommen. Der Empfang dieser Nachrichten funktioniert aber momentan mit den verfügbaren Versionen der Refbox nicht. Deshalb kann noch nicht festgestellt werden, welche Informationen ankommen und welche an den ProductController weiter geschickt müssen. Zudem muss die Klasse die entdeckten Maschinen vom ExploController erhalten, um sie der Refbox zu melden. Dies geschieht alles über den Broker. So kann sich eine andere Klasse auch die Informationen holen, falls sie diese benötigt. Die Vorteile des Brokers sind die Transparenz der Kommunikationswege und das Auffinden von Fehlern. Nebst den Klassen kann nämlich auch von ausserhalb ein Laptop auf den Broker zugreifen und die Nachrichten eines bestimmten Topics abgreifen. 

![VirtualBox_Netzwerk](https://gitlab.com/solidus/hefei/uploads/c414e2464b166b5ac077e637427bf729/VirtualBox_Netzwerk.png)

Während der Programmierung konnte das Programm immer wieder mit der VirtualBox getestet werden. NetBeans mit dem Programm lief auf dem Hostsystem und die Refbox selber lief auf dem Gastsystem. Über den Host-only-Adapter von VirtualBox, konnte vom Hostsystem auf das Gastsystem und umgekehrt zugegriffen werden. Vor dem Cup wurde das Programm mit dem Roboter getestet. Von ausserhalb konnte leider mit keiner Einstellung auf das Gastsystem zugegriffen werden. Die ideale Einstellung wäre den Bridge-Mode. Damit wird die Verbindung über das Hostsystem überbrückt. Somit sollte eine Verbindung auf das Hostsystem und das externe Netzwerk möglich sein. In der Schule funktionierte dies nicht. Es konnte weder auf das Hostsystem, noch auf das externe Netzwerk zugegriffen werden. Wenn diese Einstellung zu Hause ausprobiert wurde, stürzte der Swisscom-Router nach dem Start des Gastsystems ab und fiel in einen Restart-Loop. Erst wenn das Gastsystem wieder ausgeschaltet war, konnte der Router wieder aufstarten. Beim NAT-Netzwerk konnte das Gastsystem auf das externe Netzwerk zugreifen, aber nicht auf das Hostsystem. Beim Host-only-Adapter geschah das Gegenteil. Der Zugriff auf das Hostsystem war möglich, aber nicht den Zugriff auf das externe Netzwerk. So wurde für die Aktualisierungen des virtuellen Computers und der Refbox das NAT-Netzwerk benötigt und für die Tests wurde auf den Host-only-Adapter umgestellt. Da nun die Kommunikation zwischen Roboter und virtuellem Computer mit Refbox nicht lief, wurde die ComRefBox auf dem Hostsystem gestartet. Da alle nötigen Meldungen auf den Broker gesendet werden, war dies kein Problem. Beim Cup musste die Klasse dann im Roboter integriert werden. Ab da hatten wir dann nur noch die Möglichkeit mit der offiziellen Refbox zu testen. Dieser Umstand wurde im Vornherein nicht bedacht, dass wir selber eine Refbox für Tests haben sollten. 

![VirtualBox_Refbox_Kommunikation](https://gitlab.com/solidus/hefei/uploads/f91a9418f3e84d858e86cc389564d8ef/VirtualBox_Refbox_Kommunikation.png)

## Laserscanner
Zuerst muss man sich im bestehenden Code schlau machen. Der ist leider sehr schlecht kommentiert, sodass das eher zeitaufwändig ist. Es sind viele einzelne Funktionen vorhanden, die aber alleine nicht viel bringen. So gibts jetzt eine neue Klasse [Laserscanner](Laserscanner). Darin sind alle Funktionen zusammen, welche für das verfahren und die Exploration nötig sind.  
## StateMachine
Da es unterschiedliche Spielphasen gibt (Setup, Exploration, Produktion), ist ein gesamtes Diagramm schwierig zu erstellen. Also werden einzelne Diagramme zu den Spielphasen erstellt. Die Spielphasen wechseln sowieso unmittelbar nach der Meldung durch die Refbox. Nach dem erstellen der Diagramme für die Setupphase und für die Explorationsphase wird ein grobes Gerüst gemacht. Dieses besteht besteht aus Switch Cases mit Strings der Unterzustände. Da wird Schritt für Schritt dann der Code einprogrammiert.


