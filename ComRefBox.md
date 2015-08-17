# Klasse ComRefBox

----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 11. Juli 2015  
Version: 2.0  
Quellen:  [Google Developers](https://developers.google.com/protocol-buffers/docs/overview) | [Wikipedia, Protocol Buffers](https://de.wikipedia.org/wiki/Protocol_Buffers) [Wikipedia, Zeitstempel](https://de.wikipedia.org/wiki/Zeitstempel)

----
- <a href="#SM1.0">Aufbau der Klasse während der Diplomarbeit vor dem Cup</a>
	- <a href="#SM1.1">Methode ComRefBox</a>
	- <a href="#SM1.2">Klasse SendBeacon</a>
	- <a href="#SM1.3">Methode recvBeacon</a>
	- <a href="#SM1.4">Methode gameState</a>
	- <a href="#SM1.5">Methode infoExploration</a>
	- <a href="#SM1.6">Methode infoMachines</a>
	- <a href="#SM1.7">Methode recvOrder</a>
	- <a href="#SM1.8">Methode sendDoneJobs</a>
	- <a href="#SM1.9">Methode sendMachines</a>
	- <a href="#SM1.10">Override Methode messageArrived</a>
- <a href="#SM2.0">Die Änderungen in der Klasse ComRefBox während dem Cup</a>
	- <a href="#SM2.1">Prolog</a>
	- <a href="#SM2.2">Methode ComRefBox</a>
	- <a href="#SM2.3">Klasse SendBeacon</a>
	- <a href="#SM2.4">Methode gameState</a>
	- <a href="#SM2.5">Methode sendMachines</a>
	- <a href="#SM2.6">Override Methode messageArrived</a>
	- <a href="#SM2.7">Override Methode run</a>

----
# <a name="SM1.0">Aufbau der Klasse während der Diplomarbeit vor dem Cup</a>
Die Refbox benutzt für ihre Nachrichten Protobuf. Protocol Buffers (Protobuf) ist ein Datenformat zur Serialisierung mit einer Schnittstellen-Beschreibungssprache. Es wurde von Google entwickelt. Es ist unabhängig von Plattformen und Sprachen. Derzeit gibt es offizielle Implementierungen für Java, C++ und Python. Es ist ähnlich wie das XML, ist aber schlanker, schneller und einfacher zu handhaben. Das Nachrichtenformat wird dabei ein einer .proto-Datei gespeichert. Mit einem Compiler können diese Dateien dann in die entsprechenden Dateien der gewünschten Sprache kompiliert werden. Zum Beispiel wird mit dem Java-Compiler das *Adressbuch.proto* in ein *AdressbuchProtos.java* kompiliert. Mit der entsprechenden API können die definierten Nachrichten dann gelesen und geschrieben werden. Die Version des Compilers und die der API sollten übereinstimmen, ansonsten kann es zu Fehlern kommen. 
Die definierten Nachrichten der Refbox sind im Refbox Manual 2015 beschrieben. 

In den Nachrichten sind alle nötigen Felder definiert. Mit Getter- und Setter-Methoden können die einzelnen Nachrichtenfelder gelesen bzw. geschrieben werden. Um die Nachrichten zu erhalten muss zunächst ein ProtobufBroadcastPeer aufgebaut werden. Mit der IP-Adresse der Refbox und dem Empfangs- und Sendeport. Der ProtobufBroadcastPeer ist eine p2p-Verbindung zwischen dem Roboter und der Refbox. Die Nachrichten werden mit dem UDP-Protokoll über einen Broadcast an alle gesendet. Da am Wettbewerb dem Betrug vorgebeugt werden soll, muss zusätzlich noch ein privater Peer gestartet werden. Dieser Peer überträgt die teamspezifischen Nachrichten verschlüsselt. Das sind zum Beispiel die Bestellungen und die gefundenen Maschinen, welche verschlüsselt übertragen werden müssen. Bei diesem Peer müssen nebst der IP-Adresse der Refbox und den Ports, auch eine Bestätigung für die Verschlüsselung, die Version der Verschlüsselung und den Schlüssel mitgegeben werden. Die Version der Verschlüsselung ist momentan 2. Der Schlüssel ist standardmässig auf *randomkey* gesetzt. Dieser Schlüssel wird während dem Wettbewerb geändert, deshalb wird der Schlüssel mit dem Config-File geändert.
> **Config-File:** Im Config-File kurz Cfg sind die Parameter eingetragen, welche sich häufig ändern können. Hauptsächlich sind es die IP-Adressen.

Nachdem der Peer aufgebaut ist, werden die gewünschten Nachrichten registriert und der ganze Peer dem ProtobufMessageHandler übergeben. Dieser Handler ist als innere Klasse in der ComRefBox-Klasse definiert. Wird ein Peer dem Handler übergeben, so prüft der Handler die ankommende Nachricht und entscheidet, um welche Nachricht es sich handelt. Die Schritte die bei einer bestimmten Nachricht ausgeführt werden sollen, wurden letztes Jahr alle in dieser Klasse programmiert. Diese habe ich nun alle herausgenommen und in eigene Methoden gepackt. Der Handler ruft nun nur noch die entsprechende Methode auf. Dies macht die Programmierung einfacher und übersichtlicher. 

## <a name="SM1.1">Methode ComRefBox</a>
Die Methode ist der Konstruktor der Klasse. In ihm werden der Logger, der Broker und der öffentliche Kanal instanziiert und aufgebaut. Um nicht eine Exception zu erhalten muss zuerst die Verbindung zum Broker und danach erst die Verbindung zur Refbox aufgebaut werden. Denn wenn die Verbindung zur Refbox zuerst aufgebaut wird, verarbeitet der ProtobufThread bereits die ankommenden Nachrichten und will diese auf den Broker schicken. Die Verbindung zum Broker ist aber zu diesem Zeitpunkt noch gar nicht aufgebaut. Der Verbindungsaufbau zur Refbox bestand noch vom letzten Jahr. Da nun noch der Broker hinzugekommen ist, wurden die beiden Codeblöcke in eigene private Methoden gepackt. Im Konstruktor wird nun nur noch der Logger instanziiert und die beiden privaten Methoden aufgerufen.
## <a name="SM1.2">Klasse SendBeacon</a>
Die Klasse SendBeacon ist, wie auch der Handler, eine innere Klasse der Klasse ComRefBox. Die Klasse ist zudem eine Unterklasse der Klasse Thread und erbt dessen Methoden. Die Klasse startet einen eigenen Thread und sendet periodisch alle zwei Sekunden ein Signal über den privaten Kanal an die Refbox. Damit weiss die Refbox, welche Roboter von wessen Team auf dem Spielfeld stehen. Im Signal werden die Zeit, eine Sequenznummer, die Roboternummer, der Robotername, der Teamname, die Teamfarbe und die Position mitgeschickt. 
Für die Zeit wird aus dem System die aktuelle Zeit in Millisekunden ausgelesen und in Sekunden umgerechnet. Die Sekunden haben derzeit etwa den Wert *1438268337*. Dieser Wert ist ungewöhnlich hoch und sieht in keiner Weise einem Wert ähnlich, aus dem wir eine Zeit herauslesen können. Das kommt daher, dass es sich um die Unixzeit handelt. Die Unixzeit ist ein Zeitstempel der seit dem 1. Januar 1970 00:00 UTC kontinuierlich, ohne Schaltsekunden, hochgezählt wird. Wird die Anzahl Sekunden überschlagsmässig in Jahre umgerechnet, ergibt es ungefähr einen Wert von 45,6 Jahren. Es gibt also nicht eine menschenlesbare Uhrzeit direkt aus. Dafür aber einen Zeitwert der bei allen Unix-Systemen gleich ist und mit dem gerechnet werden kann.
## <a name="SM1.3">Methode recvBeacon</a>
Die Refbox schickt auch ihrerseits ein BeaconSignal an alle. Daraus können wieder die gleichen Informationen herausgeholt werden, wie bei der Klasse SendBeacon gesendet werden. Mit der aktuellen funktionierenden Refbox wird diese Nachricht momentan leider nicht empfangen.
## <a name="SM1.4">Methode gameState</a>
Mit der Methode wird in erster Linie geprüft, ob bei der Refbox bereits eine Teamfarbe gesetzt wurde. Sobald die Farbe bekannt ist, wird sie gespeichert und der private Kanal wird aufgebaut. Zudem wird der Kanal wieder dem Handler übergeben und dann der BeaconSignal Thread gestartet. Ansonsten schickt die Methode periodisch den Spielzustand und die Spielphase. Um zu verhindern, dass die Meldung immer wieder auf den Broker geschickt wird, werden die Phase und der Zustand in einer Variablen gespeichert. Bei der nächsten Meldung wird überprüft, ob es immer noch die gleiche Nachricht ist, wie die zuvor in der Variable gespeichert. Falls es eine andere Nachricht ist, wird die Meldung auf den Broker geschickt und wird als letzte Phase und letzter Zustand in die Variable gespeichert.
## <a name="SM1.5">Methode infoExploration</a>
In der Methode werden die Informationen, die in der Explorationsphase nötig sind, verarbeitet. Es ist eine Liste mit allen Zonen und eine mit dem Lichtsignalmuster für die Lichtsignalampel. Bei der Zonenliste werden alle 24 Zonen mit ihrer Teamzugehörigkeit gesendet. Deshalb wird die Liste in ein 12er Array kopiert. Es werden nur die Zonen kopiert, die dem eigenen Team gehören. Die Klasse *ExploController* benötigt die Zonen in einem String mit der Form "-Z1-Z2-Z3". Deshalb werden die Zellen des Arrays zu einem String zusammen gehängt. Danach wird der String auf den Broker geschickt. Da der ExploController sehr viel früher programmiert wurde als die ComRefBox, hat sich ein kleiner Optimierungsfehler eingeschlichen. Der ExploController wandelt den String nämlich wieder in ein Array um. Dies könnte später noch optimiert werden. 
Das Lichtmuster kommt auch in einer Liste. Daraus kann auch die Nummer des Zustands herausgenommen werden. 1 für ON und 0 für OFF.

| TypeString | Rot | Orange | Grün |  
| -------- | -------- | -------- | -------- |  
| "icYH2WxI" | OFF | OFF | ON |  
| "kFd$a6xb" | OFF | ON | ON |  
| "k0XjQil7" | ON | ON | ON |  
| "hI3X_qo0" | ON | OFF | ON |  
| "u=pzCm:#" | ON | ON | OFF |  
| "By.Vyvg$" | ON | OFF | ON |  

So wird das Muster in eine HashMap gespeichert.

| Schlüssel (String) | Wert (String) |  
| -------- | -------- |  
| "001" | "icYH2WxI" |  
| "011" | "kFd$a6xb" |  
| "111" | "k0XjQil7" |  
| "101" | "hI3X_qo0" |  
| "110" | "u=pzCm:#" |   
| "101" | "By.Vyvg$" |  

Diese Map wird dann in der Methode sendMachines wieder verwendet.
## <a name="SM1.6">Methode infoMachines</a>
Die Methode gehört in die Produktionsphase. Bei diversen ausgetesteten Versionen der Refbox wurden die Maschineninfos nicht korrekt ausgegeben. Die Zonen der Maschinen waren jeweils alle auf Z1 angegeben. Zudem können die Bestellungen von der Refbox nicht empfangen werden. Da der Fokus besonders auf der Explorationsphase liegt, wurde die Programmierung zurückgelegt und wird fortgesetzt sobald die Bestellungen von der Refbox empfangen werden können.
## <a name="SM1.7">Methode recvOrder</a>
Diese Methode gehört ebenfalls in die Produktionsphase. Die Bestellungen konnten jeweils mit keiner einzigen der verschiedenen ausgetesteten Versionen der Refbox empfangen werden. Daher war es schwierig diese Methode zu programmieren, da sie nicht getestet werden konnte. Daher wurde vorgesehen am Cup mit der Refbox die Nachrichten empfangen zu können und daraus das Programm direkt am Cup zu schreiben.
## <a name="SM1.8">Methode sendDoneJobs</a>
Diese Methode gehört ebenfalls in die Produktionsphase. Sie wird programmiert sobald, die beiden Methoden infoMachines und recvOrder ausprogrammiert wurden.
## <a name="SM1.9">Methode sendMachines</a>
Wenn eine Maschine gefunden wurde wird sie als Objekt Mps auf den Broker geschickt. Aus dem Objekt kann dann die ID, die Koordinaten und das erkannte Lampenmuster als Boolean ausgelesen werden. Da die Refbox aber den Namen, die Zone und den String des Lampenmusters wissen will, müssen die Werte noch umgewandelt werden. Für die ID und die Koordinaten stellt das Objekt Mps jeweils eine Methode zur Verfügung. Mit der kann die ID in einen Name umgewandelt werden und die Koordinaten in eine Zone als String. Die Zone als String muss zusätzlich noch mit einem Case in den Datentyp Zone konvertiert werden. Die Booleans vom Lichtmuster werden mit einer verkürzten Ifelse-Bedingung in einen Integer geparst. Diese drei Integer werden dann zu einem String mit der Form "000" zusammengehängt. Damit kann der String als Schlüssel verwendet werden, um in der zuvor erwähnten HashMap (Methode infoExploration) den richtigen TypeString auszulesen. Die drei Informationen werden zu einem Objekt *Maschinenreport Eintrag* gebildet und dieses Objekt wird wiederum in einem Objekt *Maschinenreport* gebildet, welches alle Objekte *Maschinenreport Eintrag* enthält. Das Objekt *Maschinenreport* wird dann dem Peer zum Versenden übergeben. So kann sichergestellt werden, dass auch wirklich jede Maschine, welche bereits entdeckt wurde, der Refbox gemeldet wird. 
Bevor die RefBoxCom programmiert wurde hiess das Objekt Machine. Dies funktionierte aber nicht da bereits die Refbox auch ein Objekt verschickt das Machine heisst. Deshalb musste die Klasse in Mps umgetauft werden.
## <a name="SM1.10">Override Methode messageArrived</a>
Die Methode messageArrived ist eine erzwungene Methode aus dem implementierten Interface *MqttCallback*. Um neue Nachrichten von einem Topic zu erhalten, muss dieser subscribed werden (sich beim Broker melden, dass das Interesse am betreffenden Topic besteht). Sobald auf dem Broker eine neue Nachricht auf einem Topic, der subscribed wurde, erscheint, wird diese Methode aufgerufen. In der Methode wird geprüft, um welches Topic es sich bei der Nachricht vom Broker handelt. So können die spezifischen Aufgaben definiert werden. Falls ein Objekt über den Broker geschickt wird, muss dieses erst Serializable gemacht werden. 
Ein Objekt existiert nur während des Programmablaufs. Ist es Serializable, geht die Objektstruktur und die Variablenbelegung nach dem Programmablauf nicht verloren. Sind diese nur während des Programmablaufs bekannt, kann eine Methode oder eine Variable nicht von einem entfernten Ort aufgerufen werden. Das Serializable hat demnach die Aufgabe das Objekt zu sichern (persistent machen) und an anderer Stelle wieder hervorzuholen. 

# <a name="SM2.0">Die Änderungen in der Klasse ComRefBox während dem Cup</a>
## <a name="SM2.1">Prolog</a>
Es war geplant die restlichen Methoden, welche noch nicht programmiert wurden, während dem Cup weiter zu verfolgen. Leider ging dieser Plan gründlich schief. Während dem Cup zeigte sich, dass die Klasse noch etliche Mängel und Fehler aufweist. Diese Klasse ist mitunter die wichtigste Schnittstelle. Das hat man während dem Cup sehr gut gemerkt. Alle anderen hatten ihre Programme für den Cup funktionsbereit. Leider nutzte das dem Team rein gar nichts. Das Problem war, dass der Maschinenreport bei der Refbox nicht ankam und so die Punkte nicht gezählt wurden. Mit der Fehlersuche verloren wir mehr als zwei ganze, wertvolle Tage und verwehrten uns so den wohlverdienten ersten Platz. Denn das Programm kann noch so gut sein, wenn der Report nicht an die Refbox gesendet werden kann, gibt es keine Punkte.  
Anhand der folgenden Neuauflistung der betroffenen Methoden wird versucht auf die Fehler einzugehen und die Änderungen hervorzuheben. Methoden welche in diesem Abschnitt nicht erwähnt werden, wurden nicht verändert oder wurden nur zu Testzwecken abgeändert.
## <a name="SM2.2">Methode ComRefBox</a>
Im Konstruktor wird neu ein Scheduler aufgerufen der alle zwei Sekunden die run-Methode aufruft.
## <a name="SM2.3">Klasse SendBeacon</a>
In der inneren Klasse wurde vorher ein neuer Thread gestartet in dem das Beaconsignal aufbereitet und dem privaten Kanal übergeben wurde. Da dies eher eine Bastelei ist und es zu Problemen mit der run-Methode aus dem Interface Runnable gegeben hat, wurde der Code in die run-Methode verschoben. In der Methode gameState wird nun nicht mehr ein neues Objekt erzeugt. Stattdessen wird ein Boolean auf true gesetzt. Auf diesen Boolean wird entsprechend in der run-Methode zugehört. Sobald der Boolean true ist wird das Beaconsignal aufbereitet und über den privaten Kanal gesendet. Die innere Klasse SendBeacon besteht noch und wurde nun als Deprecated markiert. Die Instanziierung der Klasse steht auch immer noch in der Methode gameState, wurde aber auskommentiert und als alter Code beschrieben.
## <a name="SM2.4">Methode gameState</a>
In der Methode wurde nach dem Starten des privaten Kanals der Thread für das Beaconsignal gestartet. Nun wird nur noch ein Boolean auf true gesetzt. Sobald der Boolean auf true ist, wird in der run-Methode das Beaconsignal aufbereitet und über den privaten Kanal gesendet. Der Aufruf des Threads ist noch als alter Code vorhanden. Er wurde auskommentiert und entsprechend gekennzeichnet.
## <a name="SM2.5">Methode sendMachines</a>
Dies ist die Methode bei der die hauptsächlichen Änderungen stattgefunden haben. Wird von einem Roboter eine Maschine entdeckt, wird diese als Objekt über den Broker geschickt. Das Objekt enthält eine ID, die Koordinaten und das Lampenmuster. 

Der Name der Maschine wird aus der ID heraus gelesen. Dies kann mit der Methode idToName aus der Klasse Mps gemacht werden. Vorher war diese Methode statisch und musste direkt in der Klasse aufgerufen werden. Diese Methode muss aber nicht statisch sein, deshalb wurde es geändert und die Methode wird neu direkt vom Objekt aus aufgerufen. 
Ein weiteres grosses Problem war, dass wir die Syntax des Maschinenberichts nicht kannten. So muss für den Maschinennamen im Maschinenberichteintrag zwingend der String "C-DS" geschickt werden. Da im Maschinenbericht der Eintrag, wie auch die Teamfarbe gesetzt wird, ging ich damals davon aus, dass der String "DS" längen würde. Deshalb wurde zusätzlich in der Klasse Mps die Methode idToNameRefbox programmiert. Je nach ID wird der entsprechende String ausgelesen, in der Form "[Abkürzung Teamfarbe]-[Abkürzung Maschinennamen]". 

Aus strategischen Gründen werden bei einem Objekt Mps die Koordinaten eines Punktes gespeichert, der etwa einen halben Meter vor der Maschine steht. Je nachdem wo dann die Maschine in der Zone steht, ist der Punkt ausserhalb dieser Zone. Dies führte folglich dazu, dass wir mehr Falschmeldungen auf der Refbox erhielten. Aufgrund dessen mussten die korrekten Koordinaten der Maschine zuerst mit Trigonometrie berechnet werden, bevor mit der Methode zoneDetector die Zone ausgelesen werden konnte. 

Die Verarbeitung des Lampenmusters hat gut funktioniert. Manchmal wurde die Lampenfarbe falsch gesetzt. Dies kam aber nicht von dieser Klasse sondern von der Farberkennung. Mit der hatten wir zum Schluss auch noch einige Probleme. Zudem wurde bei jeder Entdeckung einer Maschine vom ExploController automatisch eine Zweite generiert. Dies für die andere Seite der Maschine. So kamen immer zwei Objekte Mps gleichzeitig nacheinander über den Broker. Das eine hatte die ID, die Zone und das korrekte Lampenmuster. Das andere hatte die zweite ID, die Zone und das Lampenmuster "000" per Default. Da ja auf der anderen Seite eine ID, aber keine Lampe ist. Nun kam das erste Objekt kommt an, wurde aber gleich vom zweiten Objekt mit dem falschen Muster überschrieben. Wenn dann meine Methode in der HashMap nach dem richtigen Eintrag sucht, findet er natürlich nichts, da es per Definition niemals ein Lampenmuster gibt, bei dem alle Lampen ausgeschaltet sind. Wird in der HashMap nichts gefunden, wird der Typstring null.

Da nun oftmals falsche Berichte an die Refbox geschickt wurden, bauten wir einige Sicherheiten ein. Wir haben drei Boolean auf false gesetzt. Ist entweder die ID leer oder das Case ist in den Default-Fall gegangen oder in der HashMap wurde nichts gefunden, wird der entsprechende Boolean auf true gesetzt. Ein neuer Maschinenreporteintrag wird aber erst erstellt, wenn alle Booleans auf false sind. Mit anderen Worten wird erst ein Maschinenreporteintrag erstellt, wenn der Maschinennamen, der TypeString und die Maschinenzone einen Inhalt haben. Dennoch kann es immer noch zu Falschberichten kommen, wenn die Lampenerkennung die Lampen nicht richtig erkennen kann. 

Weitere grosse Probleme hatten wir mit dem Versenden des Maschinenberichts. Zuerst haben wir herausgefunden, dass die Nachricht nur einmal über UDP versendet wird. Da bei UDP die Nachrichten ohne Übermittlungsüberprüfung gesendet werden, kann es vorkommen das einzelne Teile nicht auf der anderen Seite ankommen. Dies ist besonders gravierend bei überlasteten Netzwerke, welche besonders bei einem RoboCup zu finden sind. Deshalb wird bei UDP generell das Netz einfach mit Übermittlungen bombardiert. Die Devise ist dabei, einfach senden, egal wie oft, Hauptsache die Nachricht kommt vollständig beim Gegenüber an. Deshalb begannen wir die Nachricht in einem Thread zu verarbeiten und alle 2 Sekunden zu verschicken. Dies führte zu einem Dominoeffekt und somit zu vielen weiteren Fehlern. Zuerst versuchten wir die Nachricht mit dem Beaconsignal zu versenden. Da das Beaconsignal ja bei der Refbox ankam. Dies funktionierte aber nicht. Da wir ein Problem mit der neuen run-Methode vermuteten, schalteten wir die innere Klasse SendBeacon aus und packten dafür das Beaconsignal und die Verarbeitung des Maschinenberichts in die run-Methode. Da die Variablen für den Maschinenbericht erst in der Methode sendMaschines deklariert werden, mussten sie zuerst global bekannt gemacht werden. Leider vergassen wir die lokale Deklaration zu entfernen und ignorierten den freundlichen Hinweis darauf von NetBeans "Local variable hides a Field". So wurde zwar ein Bericht in der globalen Variable gespeichert, wurde aber durch die lokale Deklaration leer überschrieben. Die Nachricht kam dann bei der Refbox an. Die konnte damit aber dann nichts anfangen. 

Zusätzlich machten wir noch den Fehler die Erstellung des Maschinenberichts mit in die run-Methode zu packen. Dieser Fehler kam leider erst am Schluss kurz vor dem Final zum Vorschein. Das Problem ist das ein UDP-Paket für die Refbox eine maximale Grösse von 1400 Bytes haben kann. Sobald es grösser wird bricht der Peer ab und die Nachrichten können nicht mehr gesendet werden. Beim Erstellen des Berichts wird jede neue Maschine additiv zum Bericht hinzugefügt. Mit jeder neuen Maschine wird der Bericht also auch grösser. Wird er nun in der run-Methode verarbeitet, wird der Bericht alle 2 Sekunden um eine Maschine vergrössert. Dies ging am Anfang ganz gut, da wir noch nicht fähig waren mehr als eine Maschine zu erkennen. Sobald wir zwei Maschinen erkannten, wurde der Bericht zu gross und der private Peer schmierte ab. So konnten wir keine Berichte mehr schicken und auch das Beaconsignal kam nicht mehr an. Laut der Refbox waren die Roboter dann verloren, obwohl sie noch weiter explorierten. Wir dachten zuerst der Peer schmiere immer ab, weil wir ihn zu schnell mit Nachrichten bombardieren. Deshalb haben wir vor und nach dem Senden ein Thread.sleep eingebaut. Bei einem erneuten Test zeigte sich, dass es gerade eine Explorationsphase lang hält, ohne dass der Peer abschmiert. Gerade vor den Finals fanden wir den Fehler mit dem Bericht. Für das Final haben wir es noch so belassen. Jetzt wird aber nur noch die Nachricht in der run-Methode gesendet. Die Aufbereitung des Berichts und der Nachricht geschieht nun alles in der Methode sendMachines. Es wurde also noch nicht getestet, ob es wirklich funktioniert. 
## <a name="SM2.6">Override Methode messageArrived</a>
Aus irgendeinem Grund kann in dieser Methode bei der Ankunft einer Nachricht nicht eine andere Methode aufgerufen werden. Deshalb wird hier nur ein Boolean auf true gesetzt und in der run-Methode wird auf diesen Boolean die Methode aufgerufen. Vorher hatten wir noch das Problem, dass auf dem Broker jeweils immer, bei einer entdeckten Maschine, zwei Objekte ankommen. Die Inputseite und die Outputseite. Da die eine Seite keine Lampenmuster hat, braucht die Klasse zwingend nur ein Objekt. Deshalb ist in dieser Methode noch eine Überprüfung, nach der nur Objekte weiterverarbeitet werden, die ein korrektes Lampenmuster haben. Neu wurde aber für die ComRefBox ein neues Topic generiert auf dem nur die relevanten Objekte gesendet werden. Dieser Code sollte eigentlich nun nicht mehr nötig sein und wurde bereits auskommentiert und beschrieben. Es wurde aber noch nicht getestet. 
## <a name="SM2.7">Override Methode run</a>
Diese Methode war vorher leer. Nun wird über sie das Beaconsignal gesendet, sobald ein Boolean in der Methode gameState auf true gesetzt wird. Sobald der Maschinenbericht erstellt und ein Boolean in der Methode sendMachines auf true gesetzt wurde, wird der Maschinenreport gesendet. Sobald eine Objekt Mps über den Broker ankommt wird ein Boolean auf true gesetzt und die Methode ruft die Methode sendMachines mit dem Objekt als Übergabewert auf. Der Boolean wird danach wieder auf false gesetzt, dass die Methode nur dann aufgerufen wird, wenn ein neues Objekt ankommt.
Für die Programmierung muss man sich vorstellen, dass die Methode sozusagen zyklusgesteuert ist. Also ähnlich einer strukturierten Programmierung.

----
Last edited by Florian Gehrig at 11. August 2015


