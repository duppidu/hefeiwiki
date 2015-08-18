## ColorDetection

Es wurde festgestellt das ein Problem mit der Device - Wahl vom C++ Teil der Markerdedektierung bestand. Das C++ Programm gab immer einen Fehler zurück wenn die Kamera der Colordetection an war.   
Um das Device Problem zu lösen wurde eine Möglichkeit gesucht die Kamera abzuschalten. Nach langem probieren dies über Java zu lösen wurde festgestellt das ein Problem mit der aktuellen OpenCV Version besteht da auch durch null setzen der ganzen Methode wurde die Kamera nicht abgeschaltet.
Lief das Programm in einem separaten Prozess stellte die Kamera ohne Fehler wie gewünscht ab. Also wurde nach einer Lösung gesucht wie man einen separaten Prozess für diese Methode erstellen konnte.   
Es wurde dann Lösung gefunden einen neuen Prozess über ein separates .jar - File zu starten. 