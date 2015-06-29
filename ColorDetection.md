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
    
![Lifeline](https://gitlab.com/solidus/hefei/uploads/e1c974047b56d253f2a56a7f93a7f0a3/Lifeline.JPG)  
    
### Farberkennung   
  
Die Farbdedektierung wird in 2 Bildern gemacht, zum einen im normalen Bild in RGB und zum andern im HSV konvertierten Bild.  
  
#### HSV  
  
Alle Farben werden in HSV definiert. HSV ist ein Farbcode der in 3 Zahlen angeben wird.    
  
![HSV_color_space](https://gitlab.com/solidus/hefei/uploads/8028743baa238d7c90889414cbefa423/HSV_color_space.png)
![HSV_cone](https://gitlab.com/solidus/hefei/uploads/fc0c1707ccb3c582bcb3fbac5aaf187b/HSV_cone.jpg)


: 1. 	

Mit Hsv_min und Hsv_max wird die Farbe definiert

   
