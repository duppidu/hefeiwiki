[Home](home) [Back](KonzeptFL)  

----------

### Inhalt ###
- <a href="#sp">Schnittstellen Programme</a>
- <a href="#sc">Schnittstellen Code</a>

----------

### <a name="sp">Schnittstelle Programme</a> ###

- [Windows 8.0 64 Bit](https://de.wikipedia.org/wiki/Microsoft_Windows_8)
- [Windows 8.1 64 Bit](https://de.wikipedia.org/wiki/Microsoft_Windows_8)  
- [NetBeans IDE 8.0.2](http://www.oracle.com/technetwork/articles/javase/jdk-netbeans-jsp-142931.html)  
- [Java 1.8.0_45](https://blogs.oracle.com/stevenChan/entry/jre_1_8_0_45)  
- [MQTT 0.0.13](http://www.jensd.de/wordpress/?p=1780)  
- [GitLab](https://gitlab.com/)  
- [Linux Ubuntu ](https://de.wikipedia.org/wiki/Linux) 


----------

### <a name="sc">Schnittellen Code</a> ###

- Kommunikation zwischen ``Klasse 1`` und ``Klasse 2``.

| Klasse 1| Klasse 2| Beschreibung|  
| :------- | --- | :---- |
| [ExploControllLocal](ExploControllLocal)| [Drive](Drive)| Senden von [Coord](Coord)|
| [ExploControllLocal](ExploControllLocal)| [ColorDedection](ColorDetection)| Empfangen [Lampen](Lamps)|
| [ExploControllLocal](ExploControllLocal)| [Marker Dedection](Markerdetection_Markercoordinates)| Empfangen [TagID](Markerdetection_Markercoordinates)|
| [ExploControllLocal](ExploControllLocal)|[Statemachine](StateMachine)|Erhalten von [Zonen](Zones)|
| [ExploControllLocal](ExploControllLocal)|[MPS](MPS)|Senden von [MPS](MPS) zum speichern|
||||
|[ProductControllLocal](ProductControllLocal)|[MPS](MPS)|Erhalten von [Coord](Coord)|
|[ProductControllLocal](ProductControllLocal)|[ProductControllMain](ProductControllMain)|Empfangen von neuen [Jobs](ProductControllMain)|
|[ProductControllLocal](ProductControllLocal)|[Drive](Drive)|Senden von neuen [Coord](Coord)|



----------