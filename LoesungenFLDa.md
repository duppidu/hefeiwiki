[Home](home) [Back](DokuSolidus)  

----------

### Inhalt ###

- <a href="#ak">Allgemeine Kommunikation</a>
- <a href="#kk">Klassen Kommunikation</a>
	- <a href="#p2">Phase 2</a>
	- <a href="#p3">Phase 3</a>
	- <a href="#db">DB</a>
		- <a href="#prod">Product</a> 
		- <a href="#ma">MPS</a>  
		- <a href="#rbz">actParts</a>  
      - <a href="#exj">exploJobs</a>
  		- <a href="#j">Job</a>  
		- <a href="#co">coord</a> 
- <a href="#pck">Product Controll Kommunikation</a>
- <a href="#exk">Explo Controll Kommunikation
- <a href="#kd">Klassen Diagramm</a>   


----------

### <a name="ak">Allgemeine Kommunikation</a> ###


![MainCom](https://gitlab.com/solidus/hefei/uploads/66b056e53a3628f06be19debaf31ca93/MainCom.PNG)

- Jeder Robi besitzt einen Lokalen Broker. Alle [Topic's](MqttTopics)   
- Diese dienen zu der Internen Kommunikation unter den verschindenden Klassen.  
- Auf einem RaspberryPi läuft seperat ein main Broker, der die übergeordnete Kommunikation unter den 3 Robis inc Main Computer gewährleistet.  
- Auf einem main Computer laufen zwei Java Programme [ProductControllMain](ProductControllMain) und [ExploControllMain](ExploControllMain). Deren Zuständigkeit ist es, die Explorations- und Produktionsphase zu handeln und eine saubere Arbeitsaufteilung unter den Robis zu gewährleisten.    
- Die gesamte Kommunikation nach aussen läuft über ein 5GHz/2,4GHz Router welcher als Knotenpunkt dient  

----------
### <a name="kk">Klassenkommunikation</a> ###

Die Kommunikation zwischen den einzelnen Klassen sieht wie folgt aus:

![LoesungDaKorrMPSV2](https://gitlab.com/solidus/hefei/uploads/166af70be6cb6fbbc62286919cc67f17/LoesungDaKorrMPSV2.png)

- Die vier Klassen [ProductControllMain](ProductControllMain), [ProductControllLocal](ProductControllLocal), [ExploControllMain](ExploControllMain) und [ExploControllLocal](ExploControllLocal) besitzen eine Verbindung zu den beiden Brokern Main und Local mittels Wifi oder LAN
- Je nachdem welche Phase aktiv ist (Init/Explo/Product) wird die Klasse [ExploControllLocal](ExploControllLocal) oder [ProductControllLocal](ProductControllLocal) aufgerufen. 

#### <a name="p2">Phase 2</a>  
 
- Die Klasse [ExploControllLocal](ExploControllLocal) ist für das komplette Handling der ExplorationsPhase Zuständig. Diese Klasse benötigt die Klasse [Zones](Zones) Welche für die Verwaltung der Felder zuständig ist. 
- Die Klasse [ExploControllMain](ExploControllMain) ist für die Verwaltung der zu Explorierenden Felder zuständig welche sie von der Refbox erhält. Sie sortiert die Felder und versendet auf Anfrage neue Aufträge.  
- Die in der ExplorationsPhase detektierten Daten werden von der [ExploControllLocal](ExploControllLocal) gesammelt und in der [MPS](MPS) Klasse gespeichert und verwaltet.  

#### <a name="p3">Phase 3</a>  
 
- Die Klasse [ProductControllLocal](ProductControllLocal) ist für die komplette Produktionsphase zuständig und wird von der übergeordneten Klasse [ProductControllMain](ProductControllMain) bei der Koordination und Kommunikation der Roboter unterstützt.  
- Die Klasse [ProductControllLocal](ProductControllLocal) besitzt die Klasse [ProductAssembly](ProductAssembly) dessen Aufgabe es ist, die zu fertigende Produkte in Einzelne Produktionsschritte aufzuteilen. 
- Die Klasse [ProductControllLocal](ProductControllLocal) benötigt zudem die Daten der Klasse [MPS](MPS) die zuvor in der Explorationsphase von der Klasse [ExploControllLocal](ExploControllLocal) gefüllt wurde. Mithilfe dieser Klassen werden die richtigen [Koordinaten](Coords) für den nächsten Produktionsschritt auf den Broker gesendet.  

#### <a name="db">DB</a> ####

Unsere Klassen besitzen 6 verschiedene Speicherelemente.

![dbdav2](https://gitlab.com/solidus/hefei/uploads/141ad0f3e01041c37d847d57e529a174/dbdav2.png)

**<a name="prod">Product:</a>**
- ArrayList.   
- Statisch einprogrammiert.  
- Sind die einzelnen Produktionsschritte für jedes Produkt gespeichert. 
- Bsp. "Produkt 1" = BaseStation/CapStation/DeliveryStation.   

**<a name="ma">MPS:</a>**  
- Hash Map.  
- Wird Dynamisch in der Explorations Phase von [ExploControllLocal](ExploControllLocal) gefüllt. 
- Sind alle [MPS](MPS) von unserem Team abgespeichert.  

**<a name="rbz">actParts:</a>**
- Array.  
- Wird durch die Split Methode beim Nachrichtenerhalt gefüllt. 
- Sind zu explorierende [Zonen](Zones) als String gespeichert.  
- Information bekommen wir von der RefBox.  
- Bsp. Nachricht "Z1-Z2-Z3-Z7-Z12-Z20" ergibt je Zahl ein Arrayplatz

**<a name="exj">exploJobs:</a>**
- ArrayList
- Wird durch die prioritySort Methode gefüllt und geordnet
- Sind zu explorierende [Zonen](Zones) als String gespeichert.
- Informationen entnehmen wir actParts Array
- Wir verwenden eine Liste da diese einfacher zu verwalten ist. 

**<a name="j">Job:</a>**
- ArrayList.  
- Wird Dynamisch in der Productions Phase gefüllt.
- Beinhaltet alle zu Produzierende Produkte.  
- Bsp. 1,2,4,2,2,1.    

**<a name="co">coord:</a>**
- Objekt.  
- Beinhaltet X, Y und Phy eines punktes welcher in einer [Zone](Zones) liegt.
- Bsp: coord c = new [Coord](Coords)(32,32,32).  
  
----------

### <a name="exk">ExploControllKommunikation</a> ###
In der Explo Controll Kommunikation ist aufgezeigt, Wie die Einzelnen Klassen während der Explorationsphase miteinander Kommunizieren
Die verarbeiteten Informationen werden mittels Broker den entsprechenden Stellen gesendet. 
  
![ExploComDaKorrV2](https://gitlab.com/solidus/hefei/uploads/21ea78fbf4572e7d1c819ade2aa38eb7/ExploComDaKorrV2.png)
  
- Sobald die Refbox Klasse die Felder erhält, werden diese an die Klasse [ExploControllMain](ExploControllMain) weitergeleitet und verarbeitet.  
- Sind die Felder verarbetet, wird jedem Robotino ein erstes zu bearbeitendes Feld gesendet.
- Die Klasse [ExploControllLocal](ExploControllLocal) wandelt dieses Feld in ein [Coords](Coord) Objekt mit den entsprechenden Werten um. 
- Sobald die Freigabe der [StateMachine](StateMachine) (start) eintrift beginnt das Anfahren des Feldes.
- Ist der Robotino an der Position angelangt, gibt er eine Rückmeldung. Trifft diese Rückmeldung ein, wird das Erkunden des Feldes eingeleitet. 
 - Wird eine MPS erkannt, so fährt der Robotino die MPS an und gibt ebenso eine Rückmeldung
 - Wird nichts erkannt, so wird der Nächste Feldecken angefahren.  
     - Ist auch das 2 mal Fehlgeschlagen, so wird der Nächste Auftrag angefordert. 
- Ist der Robotino vor der MPS in Position gib er die nächste Rückmeldung
- Der Nächste Schritt ist das Starten der MarkerDetection um den Angeklebten Tag zu erkennen
 - Ist es ein Input Tag Wird die Maschine angefahren
 - Ist es ein Output Tag wird die andere Seite der Maschine berechnet und diesen Punkt angefahren.
- Ist der Robotino an der richtigen Stelle angelangt, wird erneut Rückgemeldet
- Diese Meldung startet die Lampenerkennung, welche ein Objekt erzeugt dieses mit den erkannten werten bestückt und versendet.  
- Erhält die StateMachine dieses Objekt wird das Rückwärtsfahren ausgelöst. 
- hat sich der Robotino etwas von der MPS entfehrnt wird bei der Klasse [ExploControllMain](ExploControllMain) ein neuer Auftrag angefordert. 
  
----------

### <a name="pck">ProductControllKommunikation</a> ###

In der Product Controll Kommunikation ist ersichtlich wie die beiden Klassen [ProductControllLocal](ProductControllLocal) und [ProductControllMain](ProductControllMain) miteinander Kommunizieren und interagieren.  
Alle verarbeiteten Informationen (neue Ziele) werden mittels Broker dem [Drive](Drive) gesendet.  

![ProduktionCom](https://gitlab.com/solidus/hefei/uploads/09112bbaa859a3604cea2f76c2154477/ProduktionCom.PNG)



- Sobald die Klasse [Drive](Drive) dem Broker auf das entsprechende [Topic](MqttTopics) einen String "backwards" sendet ist das für die Klasse [ProductControllLocal](ProductControllLocal) das Signal, dass das [Drive](Drive) einen neuen Befehl benötigt.  
- Das [ProductControllLocal](ProductControllLocal) sendet eine Job Anfrage dem [ProductControllMain](ProductControllMain).  Dies sucht nach einem speziellen Algorythmus einen geeigneten Job aus und übermittelt diesen dem [ProductControllLocal](ProductControllLocal).  
- Der neu erhaltene Job wird nun vom [ProductControllLocal](ProductControllLocal) in einzelne Arbeitsschritte aufgeteilt.  
- Die erste anzufahrende [Koordinate](Coords) wird gleich an das [Drive](Drive) weitergeleitet.  
- Auf jede weitere "backwards" Anfrage wird nun die nexte anzufahrende [Koordinate](Coords) gesendet.  
- Ist der Job komplett abgearbeitet wird von dem [ProductControllLocal](ProductControllLocal) eine neue Job Anfrage an den [ProductControllMain](ProductControllMain) gesendet.  

 
----------
### <a name="kd">KlassenDiagramm</a> ###

- Klassendiagramm mit allen Methoden  

![KlassendiaDaKorr](https://gitlab.com/solidus/hefei/uploads/fb68d38e6866cc03bd4db35a275c7540/KlassendiaDaKorr.png)


