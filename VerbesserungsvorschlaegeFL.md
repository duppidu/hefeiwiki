[Home](home) [Back](DokuSolidus)


### Inhalt ###
- <a href="#v">Vorschläge</a>
	- <a href="#a">Allgemein</a>
	- <a href="#e">Exploration</a>
		- <a href="#ep">Programm</a>
	- <a href="#p">Produktion</a>
		- <a href="#pg">Greifer</a> 
		- <a href="#pp">Programm</a>  

		

----------
### <a name="a">Allgemein</a> ###

- Ersatzteile für den kompletten Robi mitnehmen.  
- Infrarotsensoren oben am Tellerrand anbringen.  
  Die Infrarotsensoren unten sehen die Maschine nicht! Maschine steht auf Rädern!  
- Funktionierende Refbox in der Schule haben, damit das Senden und empfangen der Protokolle getestet werden kann.  
  Damit hatten wir die meisten Probleme an dem Robocup.  
- Teamfarbe aus dem Cfg File entfernen und auf die Refbox zurückgreifen oder Cfg File wird durch die Refbox angepasst.

----------
### <a name="e">Exploration</a> ###

#### <a name="ep">Programm</a> ####
- Mps Klasse aufteilen in Klasse mit Methoden zum Verwalten der Mps und in Konstrukt wie Coord zum Informationen als Objekt über den Broker zu übermitteln und keine unnötigen Methoden mitsenden
- Mps als solches abändern um das Programm zu vereinfachen. Nicht mehr 1Tag = 1Mps, sondern 1Mps= 1Mps(2 Tags, 2 Coords, 1 Lampe)
- Package Master > Klasse ExploControllMain > Methode prioritySort Sortieralgorhytmus ferfeinern

----------

### <a name="p">Produktion</a> ###

#### <a name="pg">Greifer</a> ####

- Der Greifer muss mit Servos höhenverstellbar sein.  
  Die Produkte können bei dem Transport etwas nach unten rutschen und passen dann nicht auf das nächste Band.  
- Die Angriffsfläche des Greifers muss mindestes so gross sein, dass das grösste Produkt komplett umfasst werden kann.   
  Beim Fahren kann das Produkt auseinanderfallen (Boden ist teilweise sehr uneben).  

#### <a name="pp">Programm</a> ####

- Vorsicht, komplette Produktion konnte an Cup nicht getestet werden!  
- Die Ausrichtung um das Produkt von dem Band zu greifen muss mit visueller Ausrichtung (Kamera) geschehen.  
  Der Robi stand teilweise etwas ungenau vor dem Band.  
- Das beschaffen der Extrabase muss neu überarbeitet werden funktioniert auf aktuelle weise wahrscheindlich nicht.  
- Wen ein Robi sein Produkt abgeliefert hat, und kein neuen Auftrag erhält, muss er einen Default (Koordinate wo er nicht stört)  Auftrag erhalten damit er nicht vor einer wichtigen Maschine zum Stillstand kommt.  


----------