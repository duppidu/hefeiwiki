[Home](home)  
[DokuSolidus](DokuSolidus)  
  
## Vorgehen  

## Master Klasse

Bis anhin haben wir das Programm so geschrieben, dass jeder Robi selbstständig agieren kann und so wenig wie möglich auf das W-Lan netz angewiesen ist. So das im falle einer Kommunikationsstörung oder einem Stromausfall unsere Robis noch immer selbstständig ihrer Arbeit nachgehen können.
Wir haben festgestellt, dass es in vielen fällen nützlich und in einigen sogar notwendig ist, wen wir eine Übergeordnete Kommunikation zwischen den Roboter haben. Besonderst wichtig wäre dies sobald wir in die Produktion gehen würden. Doch nicht nur dort ist es notwendig, auch wen wir schon in der Explorationsphasen die Jobs (zu explorierenden Zonen) über einen übergeordneten Computer verteilen würden. So könnten wir auch im falle das ein Roboter eine Störung hat und nicht weiterarbeiten kann sicherstellen, dass alle Zonen exploriert werden. Falls dies nicht geschehen würde, könnten wir die Produktionsphase sowieso nicht starten.   
Deshalb müssen wir für die Explorationsphase und die Produktionsphase eine Master Klasse erstellen die extern auf einem Rechner läuft und die ganze Koordination zwischen den einzelnen Roboter übernimmt.

## Job Klasse

Dadurch das wir die Master Klasse einführen, die Jobs verteilen kann, müssen wir auch eine Job Klasse haben in der alle zu erledigenden Jobs gespeichert werden. Wir müssen die Jobs nach einer Logischen Reihenfolge an die Robis weiterleiten. Es macht keinen Sinn, das ein Robi einen Job ausführt der zeitlich gar nicht mehr machbar wäre. Wir müssen gewährleisten können, dass jeder Job nur einmal ausgeführt wird. Dies erreichen wir mit einem Algorithmus, der die bereits versendeten Jobs aus der aktuellen Pendenten liste löscht.
Wir werden die Jobs nach dem Schwierigkeitsgrad sortieren lassen. So dass die einfacheren Jobs (bei denen die Zeit zur kompletten Abarbeitung noch rechen würde) zuerst abgearbeitet werden.