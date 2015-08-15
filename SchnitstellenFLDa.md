[Home](home) [Back](KonzeptFLDa)  

----------

### Inhalt ###
- <a href="#sp">Schnittstellen Programme</a>
- <a href="#sc">Schnittstellen Code</a>

----------

### <a name="sp">Schnittstelle Programme</a> ###

- [Windows 8.0 64 Bit](https://de.wikipedia.org/wiki/Microsoft_Windows_8)  
- [NetBeans IDE 8.0.2](http://www.oracle.com/technetwork/articles/javase/jdk-netbeans-jsp-142931.html)  
- [Java 1.8.0_45](https://blogs.oracle.com/stevenChan/entry/jre_1_8_0_45)  
- [MQTT 0.0.13](http://www.jensd.de/wordpress/?p=1780)  
- [GitLab](https://gitlab.com/)  
- [Linux Ubuntu ](https://de.wikipedia.org/wiki/Linux)(von der Firma Festo auf den Robotino angepasst)

Von den oben genannten Programmen sind jeweils nur die Versionen aufgelistet, welche wir zu Beginn des Projekts installiert haben. Es kann im Verlauf des Projekts zu Updates und somit zu Versionsänderungen gekommen sein. Bei einer wieterführung eines Programms, ist es auf jeden fall sinnvoll die Programme auf den aktuellsten Versionen zu halten. 


----------

### <a name="sc">Schnittellen Code</a> ###

- Kommunikation zwischen ``Klasse 1`` und ``Klasse 2``.

| Klasse 1| Klasse 2| Beschreibung|  
| :------- | --- | :---- |
| [ExploControll](ExploControll)| [Drive](Drive)| Senden von [Coord](Coord)|
| [ExploControll](ExploControll)| [ColorDedection](ColorDetection)| Empfangen [Lampen](Lamps)|
| [ExploControll](ExploControll)| [Marker Dedection](Markerdetection_Markercoordinates)| Empfangen [TagID](Markerdetection_Markercoordinates)|
| [ExploControll](ExploControll)|[Statemachine](StateMachine)|Erhalten von [Zonen](Zones)|
| [ExploControll](ExploControll)|[MPS](MPS)|Senden von [MPS](MPS) zum speichern|
||||
|[ProductControllLocal](ProductControllLocal)|[MPS](MPS)|Erhalten von [Coord](Coord)|
|[ProductControllLocal](ProductControllLocal)|[ProductControllMain](ProductControllMain)|Empfangen von neuen [Jobs](ProductControllMain)|
|[ProductControllLocal](ProductControllLocal)|[Drive](Drive)|Senden von neuen [Coord](Coord)|



----------
