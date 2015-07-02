[Home](home)   
[Back](DokuSolidus)    

----------

## Thomas

Zur Vorbereitung habe ich mich im Rulebook Informiert was für Zustände der Lampensäule relevant sind.

Um sich in die OpenCV Bibliothek einzuarbeiten suchte ich zuerst im Internet nach Programmbeispielen. Mit diesen versuchte ich durch ausprobieren die Methoden von OpenCV kennen zu lernen.   
Im Internet fand ich ein Beispiel einer Farberkennung die ich dann als Grundlage meiner Klasse genutzt habe. 
Mit diesem Programm stellte ich dann fest wie die Farberkennung in OpenCV funktioniert, ich lernte wie ich die Werte der HSV Variablen setzen musste so das ich sie auf die jeweiligen Farben einstellen konnte.  
  
Ich habe dann Schritt für Schritt das Programm so abgeändert das es für die Anwendung einer Lampensäulen Detektierung geeignet ist.  
Um die Position der Farbe auszulesen habe ich zuerst mit OpenCV Linien in die gefundene Farbe gelegt. Diese Linien konnten dann über ein Array ausgelesen werden und so konnten die Position der Anfangs-und Endpunkte ermittelt werden.


##  Simon

Als Vorbereitung vor dem Programmieren habe ich mich in die verschiedenen Themen eingelesen und viel recherchiert. Neben der ALVAR Dokumentation war die OpenCv Dokumentation essentiell, da ALVAR auf OpenCv aufbaut. Ebenfalls musste ich einige Dinge über die Handhabung im Linux System nachlesen, da ich nach Absprache mit Alain Rohr nur noch mit Linux gearbeitet habe. Grund dafür war, dass ich viel mit Hardwarezugriff, Bibliotheken usw. zu tun hatte und Windows/Linux in diesen Bereichen sich wesentlich unterscheiden. Aufgrund dessen, dass die ALVAR Bibliothek nur als C++ Version existiert, musste ich mich noch in dieses Thema einlesen.
Da die ALVAR Bibliothek komplex aufgebaut ist und das kompilieren von neu geschriebenen Programmen nicht einfach war habe ich mich dazu entschlossen, Beispielprogramme der Bibliothek für meine Zwecke abzuändern. So konnte ein ändern der Cmake Files verhindert werden.

Nachdem ich eine Möglichkeit gefunden habe die Koordinaten des Tags auszulesen, habe ich mit Bryan besprochen wie er die Daten verarbeiten möchte, da er verantwortlich ist für das Verfahren/Ausrichten.


Für die Servo Steuerung habe ich alle Informationen von der thinkerforge Website erhalten. Ich habe Programmbeispiele von thinkerforge als Inspiration für mein Programm verwendet.



