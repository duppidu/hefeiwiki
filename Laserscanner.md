## Laserscanner

Die Laserscanner-Klasse ist die Klasse, welche gebraucht wird für den Robotino.  
Sie braucht fast alle Klassen des EnvirementSensing-Packages.  
In ihr findet man die nötigen Methoden um mit dem Laser auf dem Robotino zu arbeiten. 
   
Eine wichtige Funktion der Laserscanner-Klasse ist es, eine Maschine zu erkennen  
und die Koordinaten für einen Punkt davor zu berechnen.
Eine Liste mit erkannten Linien werden dazu durch verschiedene Filter geschickt.  

| Filtername | Art | Funktion |  
| -------- | -------- | -------- |  
| MinNumberReflectionsFilter | Klasse | Filtert Linien aus die aus weniger Punkten bestehen als vordefiniert. Siehe auch: [Laser Data Handling](Laser Data Handling) |  
| WPA (Wi-Fi Protected Access) | TKIP (Temporal Key Integrity Protocol) | - |  
| WPA2 (Wi-Fi Protected Access 2) | CCMP (Counter Mode with <br> Cipher Block Chaining Message Authentication Code Protocol) | AES (Advanced Encryption Standard) |   
