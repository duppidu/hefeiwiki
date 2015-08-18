# Instructions RefBox
----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 17. August 2015  
Version: 1.0  
Quellen:  [FawkesRobotics](https://trac.fawkesrobotics.org/wiki/LLSFRefBox/Install#InstallingfromGitrepository)

----
- <a href="#SM1.0">Refbox</a>
	- <a href="#SM1.1">Verzeichnisstruktur</a>
	- <a href="#SM1.2">Arbeiten mit der Refbox</a>

----
# <a name="SM1.0">Refbox</a>
## <a name="SM1.1">Verzeichnisstruktur</a>

![Verzeichnisstruktur_Refbox_3Ebene](https://gitlab.com/solidus/hefei/uploads/e7746c506641d5fd8fc74a915fc43319/Verzeichnisstruktur_Refbox_3Ebene.jpg)

Nachdem die Refbox nach der Anleitung von [FawkesRobotics](https://trac.fawkesrobotics.org/wiki/LLSFRefBox/Install#InstallingfromGitrepository) heruntergeladen wurde, entsteht der neue Ordner "llsf-refbox". Auf dem Bild oben ist die Verzeichnisstruktur bis zur zweiten Ebene dargestellt. Hauptsächlich wird das Programm **/bin/llsf-refbox** und **/bin/llsf-refbox-shell**, sowie die Konfigurationsdatei **/cfg/config.yaml** und den Ordner **/src/msgs** mit den **.proto-Files** gebraucht. 
## <a name="SM1.2">Arbeiten mit der Refbox</a>

![Refbox_nach_dem_Starten](https://gitlab.com/solidus/hefei/uploads/4c5a642fc8b190c51925450081ace51f/Refbox_nach_dem_Starten.png)

In der Konsole im Ordner **bin** kann mit dem Befehl **./llsf-refbox** die Refbox gestartet werden. Sobald die Meldung **RefBox loaded and ready to run** angezeigt wird, ist die Refbox bereit und es kann eine Verbindung zu ihr aufgebaut werden. 

![Num_Shell_nach_dem_Starten](https://gitlab.com/solidus/hefei/uploads/f9fe6c405a905b8fa02e6b43bb349a5b/Num_Shell_nach_dem_Starten.png)

**(1)** Anzeige aller Logmeldungen. Je nachdem wie das Log-Level und das Debug-Level in der Konfigurationsdatei eingestellt sind, sind mehr oder weniger Logmeldungen vorhanden. Beim Log-Level besteht die Möglichkeit zwischen **info** und **debug**. Beim Debug-Level kann eine Zahl eingestellt werden. 0= keine Debug-Meldungen, 1= minimale Debug-Meldungen, 2= mehr Debug-Meldungen und 3= maximale Debug-Meldungen.  
**(2)** Anzeige von wichtigen Informationen. Z.B. wenn ein Roboter verloren wurde. Die Meldungen sind rot hinterlegt und blinken.   
**(3)** In diesem Bereich werden die Maschinen, ihr Standort und den Zustand angezeigt. In der erste Spalte steht der Maschinennamen zusammen mit der Teamfarbe (Cyan oder Magenta). In der nächsten Spalte steht der Name der Maschine ohne Teamfarbe. Es gibt eine Basestation, eine Deliverystation, zwei Ringstation und zwei Capstation. In der dritten Spalte steht der Standort (Zone 1-24)  der Maschinen. Der Standorte der Basestation und der Deliverystation sind immer die gleichen. Z4 und Z9 für das Team Cyan und Z16 und Z19 für das Team Magenta. In der vierten Spalte sind die Lampen der jeweiligen Maschinen dargestellt. In der PreGamePhase leuchten sie alle. Die letzen Spalten sind erst für die Produktionsphase von Bedeutung.  
**(4)** In diesem Feld werden alle angemeldeten Roboter mit dem Namen und der IP-Adresse angezeigt. Sobald der Roboter kein BeaconSignal mehr sendet, gilt er von der Refbox als verloren und nach 30 Sekunden definitiv als verschwunden. Sobald ein Roboter nicht mehr erreichbar ist wird der Eintrag rot unterlegt und eine Nachricht bei Pfeilnummer 2 angezeigt.   
**(5)** In diesem Feld werden grundsätzliche Informationen zum Spiel angezeigt. Der  aktuelle Status des Spiels, die aktuelle Phase des Spiels, die bereits verstrichene Spielzeit einer Phase, die erreichten Punkte pro Team und schlussendlich, welches Team gerade mit welcher Farbe am spielen ist.  
**(6)** In diesem Bereich werden die Bestellungen angezeigt. Ausser in der Produktionsphase wird dort nichts angezeigt.  
**(7)** In dieser Taskleiste sind immer die Menüs aufgelistet, welche zur Auswahl stehen. Mit F2 kann der Spielstatus und mit F3 die Spielphase verändert werden. Über F4 wird zu Beginn eines Spiels die Teams den Teamfarben zugeordnet. Unter F9 können die Roboter ausgewählt werden, um zum Beispiel eine **Maintenance** am Roboter vorzunehmen. Mit F12 kann die Lieferung einer Bestellung bestätigt werden.  

![Shell_set_State](https://gitlab.com/solidus/hefei/uploads/6e6ef6c418297fbf7f8410a91c641a4d/Shell_set_State.png)

Beim Menü State steht zur Auswahl, WAIT_START, RUNNING und PAUSED. Sobald in den RUNNING-Satus gewechselt wurde, wird automatisch die Setupphase gestartet. Den Status PAUSED kann entweder über diese Menü aufgerufen werden oder über die Leertaste. Mit einem erneuten Klick auf die Leertaste springt die Refbox wieder in den RUNNING-Status. Sobald der PAUSED-Status eingestellt ist, wird das Spiel pausiert und alle Roboter müssen sofort stillstehen. So kann im Notfall das Spiel schnell pausiert werden. 

![Shell_set_Phase](https://gitlab.com/solidus/hefei/uploads/a0797428cc1b65741b3e7a98c23a47c7/Shell_set_Phase.png)

Beim Menü Phase steht zur Auswahl PRE_GAME,  SETUP, EXPLORATION, PRODUCTION und POST_GAME. Die letzten drei Einträge sind spezielle Phasen die keinen direkten Zusammenhang zum Spiel haben. Sie sind mittlerweile in der aktuellsten Version nicht mehr vorhanden. 

![Shell_set_Team_Color](https://gitlab.com/solidus/hefei/uploads/dc3714d667530e23b389ea9d7991595f/Shell_set_Team_Color.png)
![Shell_set_Team](https://gitlab.com/solidus/hefei/uploads/8fb177bbc6be4b58874216f158cece2f/Shell_set_Team.png)

Im Menü Team kann die Farbe, für das Setzen eines Teams ausgewählt, werden. Danach erscheint eine Liste mit allen Teams, die noch nicht gesetzt wurden.

![Shell_nach_set_Team](https://gitlab.com/solidus/hefei/uploads/412adf3d0c93401d8491963f1502a437/Shell_nach_set_Team.png)

Nachdem ein Team für eine Farbe gesetzt wurde, erscheint das Team im Bereich rechts unten.

![Num_Shell_Phase_Setup](https://gitlab.com/solidus/hefei/uploads/5e0439dc9130526b4f60066179168347/Num_Shell_Phase_Setup.png)

**(1)** In der Setupphase werden die Zonen der Maschinen angegeben. Die entsprechenden Zonen stehen in den Logmeldungen und im Bereich rechts oben.  
**(2)** Für jede Maschine wird zudem in den Logmeldungen der richtige TypeString angezeigt.   

![Num_Shell_Phase_Exploration](https://gitlab.com/solidus/hefei/uploads/861fe9acc4a74b5f2f495806f0c8498f/Num_Shell_Phase_Exploration.png)

Sobald die Explorationsphase gestartet wurde, werden mit den Lampen die Lichtmuster angezeigt. Dies ist auch auf der Shell im Bereich rechts oben zu sehen. Zum Beispiel hat die Basestation das Lichtmuster "001" und die Deliverystation das Lichtmuster "111". Eine korrekt gemeldete Maschine gibt acht Punkte. Wird ein falscher Bericht gesendet, gibt es 6 Punkte Abzug. Es geht aber nicht ins Minus. Für einen korrekten Report muss die genaue Maschinenbezeichnung (z.B. M-DS), die richtige Zone und der richtige TypeString gesendet werden. Für die Maschinenbezeichnung wird nur die genaue Bezeichnung akzeptiert. Ein DS beispielsweise, wird von der Refbox gekonnt ignoriert.

![Num_Shell_Phase_Produktion_zwei_Order](https://gitlab.com/solidus/hefei/uploads/d3b59b677b143b6fe695ad3d68757b7b/Num_Shell_Phase_Produktion_zwei_Order.png)

**(1)** Die Lichter sind nun alle auf Grün geschaltet. Die Spalte mit ID bedeutet nicht ein Identifikator, sondern steht als Abkürzung für IDLE, inaktiv. Die Farben in der letzten Spalte haben wahrscheinlich etwas mit den Produktfarben zu tun. Dies konnte ich aber nicht weiter eruieren.   
**(2)** Im oberen Bereich erscheint eine blinkende Meldung, wenn eine neue Bestellung eintrifft. Das heisst nicht, dass sie auch dann gerade startet.  
**(3)** In den Logmeldungen werden die Bestellungen auch angezeigt. Eine Produkt C0 mit der Fertigungszeit von 01:12 bis 03:22.  
**(4)** Im Bereich für die Bestellungen werden sie auch angezeigt. Dort steht welche Farben zusammengesetzt werden müssen, die Produktionszeit und das Gate für die Lieferung.   

![Num_Shell_Phase_Produktion_Station_Idle](https://gitlab.com/solidus/hefei/uploads/cd0353108b300cf3e85aadea25e8e9dd/Num_Shell_Phase_Produktion_Station_Idle.png)

Wenn eine Maschine ausfällt, erscheint dies in den Logmeldungen und im Bereich oben rechts. Die Lampe leuchtet rot und der Status ist DOWN.

![Refbox_nach_beenden_der_Shell](https://gitlab.com/solidus/hefei/uploads/a9b5d18a7df59f8a5490c7a8a2d62de9/Refbox_nach_beenden_der_Shell.png)

Mit CTRL+C kann die Shell und die Refbox beendet werden. Sobald die Shell beendet wurde erscheint bei der Refbox die Meldung, Client 127.0.0.1 disconnected.

----
Last edited by Florian Gehrig at 17. August 2015
