[Home](home) [Back](DokuSolidus)  

----------

### Inhalt ###
- Lösung
- Allgemeine Kommunikation
- Klassen Kommunikation
- Product Controll Kommunikation



----------
### Lösung ###



----------

### Allgemeine Kommunikation ###


![MainCom](https://gitlab.com/solidus/hefei/uploads/66b056e53a3628f06be19debaf31ca93/MainCom.PNG)

Jeder Robi besitzt einen Lokalen Broker. Alle [Topic's](MqttTopics)   
Diese dienen zu der Internen Kommunikation unter den verschindenden Klassen.  
Auf einem RaspberryPi läuft seperat ein main Broker, der die übergeordnete Kommunikation unter den 3 Robis inc Main Computer gewährleistet.  
Auf einem main Computer läuft ein kleines Java Programm [ProductControllMain](ProductControllMain), dessen Zuständigkeit es ist, die Produktionsphase zu handeln  
und die saubere Arbeitsaufteilung unter den Robis gehandelt wird.    
Die gesamte Kommunikation läuft über ein 5GHz/2,4GHz Router über den auch die Informationen der Refbox empfangen werden.  

----------

### Klassenkommunikation ###

Die Kommunikation zwischen den einzelnen Klassen sieht wie folgt aus:

![Loesungen](https://gitlab.com/solidus/hefei/uploads/f1cb45b9c4ae08631722db55f34cdc5f/Loesungen.PNG)


Die beiden Klassen  [ProductControllMain](ProductControllMain) und [ProductControllLocal](ProductControllLocal) besitzen eine Verbindung zu den beiden Brokern Main und Local mittels Router über Wifi.  
Je nachdem welche Phase aktiv ist (Init/Explo/Product) wird die Klasse [ExploControll](ExploControll) oder [ProductControllLocal](ProductControllLocal) aufgerufen.
#### Phase 2  
Die Klass [ExploControll](ExploControll) ist für das komplette Handling der ExplorationsPhase Zuständig. Diese Klasse benötigt unbedingt die Klasse [Zones](Zones) die für die Verwaltung der Felder zuständig ist.  
Die in der ExplorationsPhase Dedectierten [Maschinen](Machine) werden in der [Maschinen](Machine) Klasse gespeichert und verwaltet.  
#### Phase 3  
Die Klasse [ProductControllLocal](ProductControllLocal) ist für die komplette Produktionsphase zuständig und wird von der übergeordneten Klasse [ProductControllMain](ProductControllMain) bei der Koordination und Kommunikation der Roboter unterstützt.  
Die Klasse [ProductControllLocal](ProductControllLocal) Besitzt die Klasse [ProductAssembly](ProductAssembly) dessen Aufgabe es ist, die zu fertigende Produkte in Einzelne Produktionsschritte aufzuteilen. 
Die Klasse [ProductControllLocal](ProductControllLocal) benötigt zudem die Daten der Klasse [Machine](Machine) die zuvor in der Explorationsphase von der Klasse [ExploControll](ExploControll) gefüllt wurde. Mithilfe dieser Klassen werden immer die richtigen [Koordinaten](Coords) auf den Broker gesendet.


----------

### ProductControllKommunikation ###

In der Product Controll Kommunikation ist ersichtlich wie die beiden Klassen [ProductControllLocal](ProductControllLocal) und [ProductControllMain](ProductControllMain) miteinander Kommunizieren und interagieren.  
Alle verarbeiteten Informationen (neue Ziele) werden mittels Broker dem [Drive](Drive) gesendet.  

![ProduktionCom](https://gitlab.com/solidus/hefei/uploads/09112bbaa859a3604cea2f76c2154477/ProduktionCom.PNG)



Sobald die Klasse [Drive](Drive) dem Broker auf das entsprechende [Topic](MqttTopics) einen String "backwards" sendet ist das für die Klasse [ProductControllLocal](ProductControllLocal) das Signal, dass das [Drive](Drive) einen neuen Befehl benötigt.  
Das [ProductControllLocal](ProductControllLocal) sendet eine Job Anfrage dem [ProductControllMain](ProductControllMain).  Dies sucht nach einem speziellen Algorythmus einen geeigneten Job aus und übermittelt diesen dem [ProductControllLocal](ProductControllLocal).  
Der neu erhaltene Job wird nun vom [ProductControllLocal](ProductControllLocal) in einzelne Arbeitsschritte aufgeteilt.  
Die erste anzufahrende [Koordinate](Coords) wird gleich an das [Drive](Drive) weitergeleitet.  
Auf jede weitere "backwards" Anfrage wird nun die nexte anzufahrende [Koordinate](Coords) gesendet.  
Ist der Job komplett abgearbeitet wird von dem [ProductControllLocal](ProductControllLocal) eine neue Job Anfrage an den [ProductControllMain](ProductControllMain) gesendet.  

 
----------




----------