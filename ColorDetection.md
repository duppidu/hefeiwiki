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
  
  
- Die erste Zahl gibt durch einen Winkel an um welche Farbe es sich handelt  
- Die zweite Zahl definiert die Sättigung der Farbe
- Die dritte Zahl definiert die Helligkeit         
      
  
       
Die Farbe wird in ein Scalar gespeichert in diesem können die drei Werte in einem bereich von 0-255 gespeichert.   
Das bedeutet dass die Werte konvertiert werden müssen sprich für die Farbe 360° = 255 und in der Sättigung und Helligkeit 100% = 255.	

Mit Hsv_min und Hsv_max wird die Farbe definiert. Im unkonvertierten Bild wird nun überprüft welche Farbe in der Tolleranz von Hsv_min und max liegt danach wird das Bild in ein HSV Bild Konvertiert und die gleiche überprüfung mit Hsv2_min und Hsv2_max gemacht.  
Nach dieser Überprüfung welche Farbe in beiden Bildern am gleichen Ort vorhanden ist.  



   
