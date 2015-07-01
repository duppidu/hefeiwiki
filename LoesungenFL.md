[Home](home) [Back](DokuSolidus)  

----------

### Inhalt ###
- Lösung
- Allgemeinekommunikation
- Klassenkommunikation
- 

----------
### Lösung ###



----------

### Allgemeine Kommunikation ###


![MainCom](https://gitlab.com/solidus/hefei/uploads/66b056e53a3628f06be19debaf31ca93/MainCom.PNG)

Jeder Robi besitzt einen Lokalen Broker. [Topic's](MqttTopics)   
Diese dienen zu der Internen Kommunikation unter den verschindenden Klassen.  
Auf einem RaspberryPi läuft seperat ein main Broker, der die übergeordnete Kommunikation unter den 3 Robis inc Main Computer gewährleistet.  
Auf einem main Computer läuft ein kleines Java Programm [ProductControllMain](ProductControllMain), dessen Zuständigkeit es ist, die Produktionsphase zu handeln  
und die saubere Arbeitsaufteilung unter den Robis gehandelt wird.    
Die gesamte Kommunikation läuft über ein 5GHz/2,4GHz Router über den auch die Informationen der Refbox empfangen werden.  

----------

### Klassenkommunikation ###

Die Kommunikation zwischen den einzelnen Klassen sieht wie folgt aus:

![Loesungen](https://gitlab.com/solidus/hefei/uploads/f1cb45b9c4ae08631722db55f34cdc5f/Loesungen.PNG)

----------


----------
### UML ###



----------