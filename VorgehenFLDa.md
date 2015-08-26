[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

## Master Klasse

Bis anhin haben wir das Programm so geschrieben, dass jeder Robi selbstständig agieren kann und so wenig wie möglich auf das W-Lan netz angewiesen ist. So das im falle einer Kommunikationsstörung oder einem Stromausfall unsere Robis noch immer selbstständig ihrer Arbeit nachgehen können.
Wir haben festgestellt, dass es in vielen fällen nützlich und in einigen sogar notwendig ist, wen wir eine Übergeordnete Kommunikation zwischen den Roboter haben. Besonderst wichtig wäre dies sobald wir in die Produktion gehen würden. Doch nicht nur dort ist es notwendig, auch wen wir schon in der Explorationsphasen die Jobs (zu explorierenden Zonen) über einen übergeordneten Computer verteilen würden. So könnten wir auch im falle das ein Roboter eine Störung hat und nicht weiterarbeiten kann sicherstellen, dass alle Zonen exploriert werden. Falls dies nicht geschehen würde, könnten wir die Produktionsphase sowieso nicht starten.   
Deshalb müssen wir für die Explorationsphase und die Produktionsphase eine Master Klasse erstellen die extern auf einem Rechner läuft und die ganze Koordination zwischen den einzelnen Roboter übernimmt.
