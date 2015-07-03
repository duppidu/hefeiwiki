[Home](home) [Back](KonzeptFL)  

----------

### Inhalt ###

- <a href="#v">Visuell</a>
- <a href="#m">Materiell</a>
- <a href="#e">Ergebnis</a>
	- <a href="#k1">Klasse 1</a>
	- <a href="#k2">Klasse 2</a>
	- <a href="#k3">Klasse 3</a>
- <a href="#com">Kommunikation</a>

----------
### <a name="v">Visuell</a> ###

Wir haben die Internen Videos des letztjährigen Robocup und die vorhandenen Videos im [Yotube](https://www.youtube.com/results?search_query=robocup+2014+logistics+league) Analysiert.  
Mögliche Funktionen erkannt und ausgewertet.   

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://www.youtube.com/watch?v=J-5QzhGg4ls)


----------

### <a name="m">Materiell</a> ###

Wir haben das [`RuleBook`](http://www.robocup-logistics.org/rules/rulebook2015.pdf?attredirects=0&d=1) durchgelesen und Analysiert.    

----------


### <a name="e">Ergebnis</a> ###

![Ideen](https://gitlab.com/solidus/hefei/uploads/4a56788e0908c8e418d145f45fbb2c49/Ideen.PNG)

Das Spiel besteht aus 3 verschiedenen Phasen. Wobei wir erst in den zwei letzten Phasen zum tragen kommen.
- Start Up
- Explorationsphase
- Productionsphase

Wir benötigen im ganzen 3 Haupttklassen.  

#### <a name="k1">Klasse 1:</a>  
Handelt die Explorationsphase
 - Koordinieren von Robotinos 
- Welcher Robi sucht wo nach Maschinen    
  
#### <a name="k2">Klasse 2:</a>  
Handelt die Productionsphase
 - Koordinieren von Robotinos
- Welcher Robi Produziert wo  
- Welcher Robi Produziert wann     
- Welcher Robi Produziert was 

#### <a name="k3">Klasse 3:</a>   
Handelt das komplette Feld inc Maschinen.  
- Verwalten von Zonen  
- Speichern der Maschinen
- Verwalten der Maschinen

#### <a name="com">Kommunikation</a> #####

- Die Kommunikation Intern wird mittels MQTT im Robotino gewährleistet.  
- Die Kommunikation Extern wird mittels MQTT auf einem extrenen Computer gewährleistet.


----------