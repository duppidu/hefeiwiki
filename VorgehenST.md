[Home](home)   
[Back](DokuSolidus)    

----------

## Thomas

Zur Vorbereitung habe ich mich im Rulebook Informiert was für Zustände der Lampensäule relevant sind.

Um sich in die OpenCV Bibliothek einzuarbeiten suchte ich zuerst im Internet nach Programmbeispielen. Mit diesen versuchte ich durch ausprobieren die Methoden von OpenCV kennen zu lernen.   
Im Internet fand ich ein Beispiel einer Farberkennung die ich dann als Grundlage meiner Klasse genutzt habe. 
Mit diesem Programm stellte ich dann fest wie die Farberkennung in OpenCV funktioniert, ich lernte wie ich die Werte der HSV Variablen setzen musste so das ich sie auf die jeweiligen Farben einstellen konnte.  
  
Ich habe dann Schritt für Schritt das Programm so abgeändert das es für die Anwendung einer Lampensäulen Detektierung geeignet ist.  
Um die Position der Farbe auszulesen habe ich zuerst mit OpenCV Linien in die Gefundene Farbe gelegt. Diese Linien konnten dann über ein Array ausgelesen werden und so konnten die Position der Anfangs-und Endpunkte ermittelt werden.


