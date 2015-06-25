# Color Detection  
  
Beim instanzieren des Programms wird die Kamera gestartet und das Kamera-bild auf eine Matrix gelegt.
Die Methode messageArrived() wartet auf eine Nachricht auf dem Color Topic des Brokers, falls die Nachricht einen String mit dem Inhalt "start" beinhaltet startet die Farbüberprüfung.  

Nun wird in der run() Methode trackColor gestartet.  

Die Methode trackColor() wird nun 40 mal für jede Farbe im 50ms Takt aufgerufen.   
Beim überprüfen wir nur Leuchten detektiert, zum eingrenzen welche Lampe das leuchtet wird die Position des lichtes überprüft.  
  
Nachdem jede Farbe überprüft wurde wird in lightAnalyze() analysiert wie oft Licht in dem entsprechenden Feld detektiert wurde.  
  
 **Nicht Leuchten**  
Wird in unter 10% der Fälle Licht detektiert giltet die Lampe als nicht Leuchtend.  
  
**Blinken**  
Wir in ca der hälfte der Fälle Leuchten dedektiert blinkt die Lampe.  
  
**Leuchten**  
Wird in ca 90% der Fälle Leuchten detektiert Leuchtet die Lampe.  
  
  
### trackColor()  
  
In der Methode trackColor wird die ganze Bildumwandlung gemacht und in einem Switch Case dan nach der jeweiligen Farbe gesucht. Bei Aufruf dieser Methode wird die Farbe nur einmal überprüft.   



