[Home](home) [Back](KonzeptFL)  

----------

### Inhalt ###
- <a href="#sp">Schnitstellen Programme</a>
- <a href="#sc">Schnitstellen Code</a>

----------

### <a name="sp">Schnittstellen Programme</a> ###

- Windows 8.0 64 Bit  
- NetBeans IDE 8.0.2  
- Java 1.8.0_45  
- MQTT 0.0.13  
- GitLab  
- Linux Ubuntu


----------

### <a name="sc">Schnittellen Code</a> ###


| Klasse 1| Klasse 2| Beschreibung|  
| :------- | --- | :---- |
| [ExploControll](ExploControll)| [Drive](Drive)| Senden von [Coord](Coord)|
| [ExploControll](ExploControll)| [ColorDedection](ColorDetection)| Empfangen [Lampen](Lamps)|
| [ExploControll](ExploControll)| [Marker Dedection](Markerdetection_Markercoordinates)| Empfangen [TagID](Markerdetection_Markercoordinates)|
| [ExploControll](ExploControll)|[Statemachine](StateMachine)|Erhalten von [Zonen](Zones)|
| [ExploControll](ExploControll)|[Machine](Machine)|Senden von [Machine](Machine) zum speichern|
||||
|[ProductControllLocal](ProductControllLocal)|[Machine](Machine)|Erhalten von [Coord](Coord)|
|[ProductControllLocal](ProductControllLocal)|[ProductControllMain](ProductControllMain)|Empfangen von neuen Jobs|
|[ProductControllLocal](ProductControllLocal)|[Drive](Drive)|Senden von neuen [Coord](Coord)|



----------