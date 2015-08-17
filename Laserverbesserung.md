[Back](VerbesserungsvorschlaegeMFT)  
[Home](home)  
## Verbesserung der Maschinenerkennung durch den Laserscanner

Während der Entwicklung funktionierte die Maschinenerkennung sehr zuverlässig.  
Am Robocup tauchte das Phänomen auf, dass der Laserscanner offensichtlich gut sichtbare Maschinen nicht als solche erkannt wurden.
Zum Beispiel musste der Robotino in den zweiten oder dritten Ecken der Zone fahren um die Maschine zu erkennen, obwohl sie in der ersten Ecke gut erkennbar war.  

![Unregelmässigkeit](https://gitlab.com/solidus/hefei/uploads/df8fd4338994055c5ac48a2811c451ba/Unregelmässigkeit.JPG)
Solche Unregelmässigkeiten 

Dies könnte folgende Ursachen haben:  
- Der Akku des Robotinos hatte nicht mehr genug Spannung für den Laser
- Die Maschinenwände am Robocup waren aus Metall, beim testen aus Holz. (Metall = verstreute Reflektionen)
- Allgemein ungenauer Laserscanner  

### Lösungsvorschläge

Es ist allgemein eine gute Idee, noch einmal die Filterklassen des Laserscanners zu kontrollieren und auf allfällige Fehler zu überprüfen. Wenn dies keine Verbesserung bringt, ist ein anderer Laserscanner empfehlenswert. Entweder hat dieser eine höhere Auflösung (mehr Messpunkte), weniger Toleranz bei der Messung oder beides.
