# Verbesserungen ComRefBox
Zuerst eine Sammlung von Problemen, die meisten sind am Cup selber vorgekommen, viele vor dem Cup während der Diplomarbeit und ein paar sind auch vorher bereits erschienen.   

**Protobuf API auf Robotino**  
Die API's werden nicht mit dem jar auf den Robotino geladen. Als die ComRefBox im Programm auf dem Robotino integriert wurde, gab es immer beim Starten eine Exception. Nach längerer Problemsuche kam zum Vorschein, dass die API's separat auf den Robotino geladen werden müssen. Dort war aber noch die Version 2.5.0 anstatt die aktuelle Version 2.6.1. Nachdem die alte API durch die Neue ersetzt wurde, gab es keine Exception mehr und das Programm konnte gestartet werden.  

**Local Variable hides a field**  
Bei den Änderungen an der ComRefBox wurde eine Variable verschoben. Diese Variable war nun nicht mehr in der gleichen Methode wie vorher, brauchte aber einen Wert einer Variable aus dieser Methode. Diese Variable wurde vorher lokal deklariert und initialisiert. Nun musste sie global bekannt gemacht werden (global deklarieren), dass die verschobene Variable deren Wert abrufen kann. Nun wurde aber vergessen die lokale Deklaration zu entfernen. NetBeans macht einem mit einem Warnhinweis darauf aufmerksam, "Local Variable hides a field". Wie so oft wurde der Warnhinweis ignoriert. Dadurch wurde aber die globale Variable von der Lokalen immer wieder überschrieben.   

**Aufruf von Verbindungen Broker - Refbox**  
Im Konstruktor wurde zuerst die Verbindung zur Refbox aufgebaut und gleich danach die Verbindung zum Broker. Nun gab es aber immer wieder komische widersprüchliche Exceptions. Der Fehler war enorm schwierig zu finden, alleine wurde das nicht geschafft. Umso einfacher war die Lösung. Sobald die Verbindung zur Refbox aufgebaut ist, startet ein neuer Thread, der empfängt und verarbeitet bereits die ankommenden Nachrichten. Währenddessen ist der Broker am Aufstarten. Der Thread möchte bereits die verarbeiteten Nachrichten auf den Broker schicken, der braucht aber etwas länger und ist noch nicht bereit. Deshalb gibt es beim Senden einen Fehler, da die Verbindung noch nicht steht. Mit der umgekehrten Reihenfolge funktioniert es nun tadellos.  

**Firewall vom Robotino deaktivieren**  
Wegen den Kommunikationsproblemen mit der Refbox, wurde der Tipp gegeben beim Robotino mit dem Befehl "sudo iptables -F" die Firewall des Robotinos auszuschalten. Dies muss entweder nach jedem neuen Start geschehen oder es wird direkt in ein Start-Skript geschrieben. Wir haben es immer manuell gemacht. Wir haben aber nie getestet, welche Auswirkungen es wirklich hatte.   

**Falscher String für Maschinenbericht**  
Im Maschinenbericht wurde für den Maschinennamen der String, "BS" für Basestation, geschickt. Für eine korrekte Ablieferung des Berichts muss der String aber in der Form, "M-BS" für Basestation von Magenta, sein.   

**Objektaufruf im messageArrived**  
In der Methode messageArrived vom Broker können keine Objekte aufgerufen werden. Stattdessen muss eine Variable gesetzt werden, mit der die Methode an einem anderen Ort aufgerufen werden kann.  

**Gleicher Benutzer für Anmeldung bei Broker**  
Zuerst wurde die ComRefBox immer nur einmal lokal auf dem Laptop gestartet. Da spielte die Wahl des Benutzers keine Rolle. Als dann die Klasse im Programm integriert wurde, gab es drei gleiche Benutzer auf dem Broker. Das ist unzulässig. Deshalb musste der Benutzername mit der Roboternummer aus dem Config-File ergänzt werden. So gibt es drei unterschiedliche Benutzer.  

**Ports für die Verbindung zur Refbox**  
Die Refbox kann wahlweise über denselben oder über zwei verschieden Ports senden und empfangen. Diese Einstellung kann auch im Config-File der Refbox eingestellt werden. Bei der ComRefBox steht dazu eine Variable zur Verfügung (Boolean local). Wenn der Booelan false ist, wird nur ein Port für die Kommunikation verwendet. Falls der Boolean true ist, wird für das Senden und Empfangen jeweils ein separater Port verwendet. Die Entscheidung welche Ports verwendet werden funktioniert über eine verkürzte Ifelse-Abfrage. Diese Art war mir damals völlig unbekannt, deshalb wurde dem zu wenig Aufmerksamkeit geschenkt. Es ist aber wichtig zu beachten, da je nach Einstellung die Verbindung zur Refbox nicht funktioniert.    

**Kein aktuelles Manual von der Refbox**  
Bis kurz vor dem Wettbewerb war kein Manual der diesjährigen Refbox vorhanden. Darum orientierte man sich am Manual vom letzten Jahr. Es konnte darauf ausgegangen werden, dass sich die meisten Nachrichten nicht geändert haben. Einige Informationen können auch aus den Proto-Files heraus gelesen werden. Diese sind bei der Refbox immer dabei, weshalb sie auch immer aktuell sein sollten. Am meisten Nutzen brachte, die ankommenden Nachrichten mit einem Logger auszulesen. So konnte am Besten herausgefunden werden was die Nachrichten enthalten und wie diese am Besten verarbeitet werden sollten.  

**Die Refbox lief nicht auf einem Ubuntu**  
Die Refbox sollte anfangs auf einem Ubuntu laufen. Ubuntu ist einfacher zu handhaben, im Internet findet man mehr Informationen und laut dem Programmierer der Refbox soll sie auf einem Ubuntu laufen. Beim Kompilieren gab es aber immer wieder ein Fehler. Deshalb wurde doch auf Fedora gewechselt.  

**Die neueren Versionen liefen nicht mehr auf einem Fedora**  
Die älteren Versionen (April/Mai) liefen auf einem Fedora. Mit der neuen Versionen traten aber verschiedene Probleme auf. So konnten sie zum Teil nicht einmal kompiliert werden. Wenn der Kompiliervorgang einmal erfolgreich ausgeführt wurde, konnte dafür die Shell nicht gestartet werden oder es zeigte die Roboter in der Shell nicht an. Da damit nicht gearbeitet und getestet werden konnte, wurde mit der alten Version weitergearbeitet. Da war VirtualBox extrem praktisch. Es konnten gleich verschiedene Systeme für einen Test der Installation bereitgestellt werden. Sobald die eine Installation funktionierte konnte diese weggestellt werden. Danach konnte ein neuer Computer erstellt werden, um dort weiter zu experimentieren.   

**Integration im Robotino**  
Am Cup musste früher oder später die ComRefBox im Programm des Robotinos integriert werden. Danach konnte nicht mehr mit der eigenen Refbox getestet werden, da ja die Verbindung zur VirtualBox von aussen nicht funktionierte. Folglich kam die Abhängigkeit zur offiziellen Refbox. Diese stand aber nicht immer zur Verfügung, da der Programmierer oftmals Analysen und Verbesserungen an der Software vornehmen musste.   

**Bestellinformationen**  
Irgendwo gibt es noch einen grossen Fehler. Er konnte aber bisher noch nicht lokalisiert werden. Die Maschineninformationen in der Produktionsphase konnten immer empfangen werden. Bei diversen getesteten Versionen und der offiziellen Version der Refbox kamen sie korrekt an. Bei anderen getesteten Versionen der Refbox kamen die Informationen falsch an. Dies zeigte sich indem bei der Zone alle Maschinen auf Z1 angegeben waren. Bei keiner einzigen Version, nicht einmal bei der offiziellen Version konnten die Bestellinformationen empfangen werden. Es ist nicht klar, ob es an den Proto-Files liegt oder im Code selber, z.B. bei der Registratur der Nachricht.  

**Image aufspielen**  
Das Image kann mit PartImage nicht auf eine kleinere Partition aufgespielt werden. Das war besonders das Problem, als wir einen Ersatzrobotino erhielten. Die Schule selber hat drei grosse Modelle des Robotinos mit einem 64GB-Speicher. Der Ersatzrobotino war das kleinere Modell und hatte nur einen 32GB-Speicher. Ein Systemstart über den USB-Stick hat auch nicht funktioniert, es war zu langsam.  

### Verbesserungsvorschläge
**Logs der Refbox**  
Lernen wie die Logs der Refbox aufgebaut sind und wie sie gelesen werden können. Das wäre praktisch als zusätzliche Quelle für die Fehlersuche. Am Cup wäre dies von Vorteil gewesen, wurde aber zu wenig angeschaut.  

**Änderungen akustisch aufzeichnen**  
Während des Cups kann es sehr gut vorkommen, dass viele Änderungen in relativ kurzer Zeit gemacht werden müssen. Auch der Beste mag, bei diesem Druck, nicht alle Änderungen im Detail aufschreiben. Deshalb wäre es eventuell leichter die Änderungen akustisch zu dokumentieren.  

**Eigene Refbox mit externem Zugriff**  
Eine laufende Refbox während dem Cup ist zwingend nötig. Mit dem Robotino muss dabei auf die Refbox zugegriffen werden können. Entweder findet sich eine Lösung mit der VirtualBox, was zu bevorzugen wäre oder es steht ein Laptop zur Verfügung. Anstatt des klobigen Laptops wäre dann eventuell auch ein Blick auf das Raspberry von Nutzen.  

**Programmierung früher beginnen**  
Zuerst wurde sehr viel Zeit aufgebracht, um sich in die Funktion der Refbox und in den bestehenden Code einzulesen. Der Plan war alles gut zu studieren, dass die Materie gut beherrscht wird und der Code von Anfang an sauber aufgebaut werden kann. Im Nachhinein wurde viel Zeit damit verloren, besser einfach einmal loslegen. Das wird aber nächstes Jahr bestimmt weniger das Problem sein, da nun sehr gute Anleitungen und Kommentare bereitstehen.  

**Bestellinformationen**  
Die Bestellinformation konnten bisher nie empfangen werden. Deshalb war es auch schwierig den Code dazu zu programmieren, wenn nicht mit einem Logger der Inhalt der Nachricht gelesen werden konnte, um zu sehen in welchem Format die Informationen ankommen. Diesem Umstand muss noch nachgeforscht werden.  

**JavaDoc**  
Es wäre hilfreich, wenn das Schreiben der JavaDoc ein Teil des regulären Unterrichts werden würde.  

**Neuer Robotino**  
Falls ein neuer Robotino ankommt, sollte davon ausgegangen werden, dass dieser entlehnt wurde. Deshalb immer zuerst ein Backup des Betriebssystems erstellen. Ansonsten kann es zu unnötigem Aufwand führen.  


