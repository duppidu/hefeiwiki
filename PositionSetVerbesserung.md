[Back](VerbesserungsvorschlaegeMFT)  
[Home](home)  
***
## Verbesserungsvorschlag für die Positionssetzungsprodezur
Die [Positionssetzung](PositionSet) wurde am RoboCup 2015 verändert. Die aktuelle Methode funktioniert zwar einigermassen, es kann aber am Anfang zu Zusammenstössen zwischen den Robotinos kommen. Ausserdem müssen sie immer sehr exakt auf den richtigen Punkt gesetzt werden, was kostbare Zeit kosten kann. Um dieses Problem zu beheben gibt es mehrere Ansätze:

#### Laserpositionierung erweitern

![ablauf](https://gitlab.com/solidus/hefei/uploads/580ccaf79dd38b0570ea1b8fe9538a2f/ablauf.gif)  
Dabei wird wieder die ursprüngliche Methode benutzt und so erweitert, dass die Robotinos am Anfang der Explorationsphase wieder in dem Startbereich stehen.

#### Laserpositionierung verschnellern  
Dabei wird auch die ursprüngliche Methode benutzt und diese so weit verschnellert, dass sie am Anfang der Explorationsphase starten kann und nicht mehr viel Zeit verschwendet.

#### Aktuelle Methode verbessern
Dabei wird die aktuell benutzte (RoboCup 2015) soweit verbessert, dass sie mit Sicherheit keinen Crash verursachen.