[Back](VerbesserungsvorschlaegeMFT)  
[Home](home)  
***
## Verbesserung des gesamten StateHandling

Das gesamte Handling mit den States und den neuen Jobs usw. funktioniert zwar momentan zuverlässig, ist aber relativ unübersichtlich. Da sehr viele Klassen mitreden und ähnliche Aufgaben haben wie die StateMachine, wirkt das ganze unnötig aufgebläht.  
  
### Verbesserungsvorschläge

Das Konzept mit den Klassen des Packages Master und der StateMachine sollte noch einmal klar aufgezeichnet und die Aufgabenteilung stärker getrennt werden. Insbesondere für die kommende Produktionsphase mit eventuellem Restarts eines Robotinos ist dies von immenser Wichtigkeit.  
Ein Restart eines Robotinos ist auf dem aktuellen Stand unmöglich. Dies sollte in Zukunft möglich sein. Das hätte unter anderem zur Folge, dass der aktuelle Status, die Spielphase, ev. entdeckte Maschinen oder sonstiges entweder zwischengespeichert wird oder manuell beim Restart eingegeben werden kann.