[Home](home)   
[Back](DokuSolidus)    

----------

## Thomas  

Der genau Ablauf der Colordetection ist Hier zu finden:
[ColorDetection](ColorDetection)

### Testplan

**Situation:**  Die Kamera soll beim starten des Programms gestartet werden und nach erhalten des Startbefehles soll die Kameraerkennung gestartet werden.

| Klasse| Funktion | Beschreibung| I.O.| 
| :------- | --- | --- | :---- |
| Start-Up|programStartup()|Start-Up instanziert in einer Schrittkette die Color detection |X |
| ExploControll|saveMachine()|Übergabewerte statisch setzen mit sout kontrollieren ob In & Out der Maschine richtig gespeichert wurden |X |


![Testbericht_Color](https://gitlab.com/solidus/hefei/uploads/0e1fab2df30107ad4c6e44111aeff4db/Testbericht_Color.JPG)