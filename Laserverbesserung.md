[Back](VerbesserungsvorschlaegeMFT)  
[Home](home)  
## Verbesserung der Maschinenerkennung durch den Laserscanner

Während der Entwicklung funktionierte die Maschinenerkennung sehr zuverlässig.  
Am Robocup tauchte das Phänomen auf, dass der Laserscanner offensichtlich gut sichtbare Maschinen nicht als solche erkannt wurden.
Zum Beispiel musste der Robotino in den zweiten oder dritten Ecken der Zone fahren um die Maschine zu erkennen, obwohl sie in der ersten Ecke gut erkennbar war.  

Dies könnte folgende Ursachen haben:  
- Der Akku des Robotinos hatte nicht mehr genug Spannung für den Laser
- Die Maschinenwände am Robocup waren aus Metall, beim testen aus Holz. (Metall = verstreute Reflektionen)
- Allgemein ungenauer Laserscanner