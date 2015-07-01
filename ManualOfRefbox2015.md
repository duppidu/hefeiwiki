# Refbox Manual 2015

----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 15. Juni 2015  
Version: 1.0  
Quellen:  [RoboCup Logistics League](http://www.robocup-logistics.org/refbox) | [FawkesTrac](https://trac.fawkesrobotics.org/wiki/LLSFRefBox#LLSFRefereeBoxrefbox)

----
- <a href="#SM1.0">Infrastruktur</a>
	- <a href="#SM1.1">Protobuf</a>
	- <a href="#SM1.2">Framing-Protokoll</a>
		- <a href="#SM1.2.1">Frame-Kopfzeilenprotokoll</a>
		- <a href="#SM1.2.2">Nachrichtenkopf</a>
		- <a href="#SM1.2.3">Unverschlüsselte Nachrichten</a>
		- <a href="#SM1.2.4">Verschlüsselte Nachrichten</a>
		- <a href="#SM1.2.5">Verschlüsselungsmethoden</a>
	- <a href="#SM1.3">Kommunikationsmethoden</a>
		- <a href="#SM1.3.1">Kommunikationsgruppen</a>
		- <a href="#SM1.3.2">Verschlüsselungsaufbau</a>
	- <a href="#SM1.4">Beispiel für den Gebrauch der Protobuf_Comm-Bibliothek</a>
- <a href="#SM2.0">Messages</a>
	- <a href="#SM2.1">Attention Messages</a>
	- <a href="#SM2.2">Beacon Signal</a>
	- <a href="#SM2.3">Versionsinfo</a>
	- <a href="#SM2.4">Zeit</a>
	- <a href="#SM2.5">Position</a>
	- <a href="#SM2.6">Team</a>
	- <a href="#SM2.7">Explorationinfo</a>
	- <a href="#SM2.8">Spielinfo</a>
	- <a href="#SM2.9">Spielstatus</a>
	- <a href="#SM2.10">Maschinen Info</a>
	- <a href="#SM2.11">Maschinenkommandos</a>
	- <a href="#SM2.12">Maschinenbericht</a>
	- <a href="#SM2.13">Bestellung</a>
	- <a href="#SM2.14">Puckinfo</a>
	- <a href="#SM2.15">Roboterinfo</a>
	- <a href="#SM2.16">Roboterkommandos</a>

----
>Notice: This is the translating of the Refbox Manual of 2014.

# <a name="SM1.0">Infrastruktur</a>
Die Refbox kommuniziert mit zwei unterschiedlichen Kategorien von Instanzen, Roboter und Controller. Jede Maschine von einem spielenden Team wird als Roboter betrachtet. Controller werden vom Schiedsrichter verwendet um mit der Refbox zu interagieren, visualisation wird intern gelöst, und gibt so an der Refbox Instruktionen.  

Alle Kommunikationen erfolgen über IPv4. Es gibt zwei Kommunikationswege. Die Controller greifen über das TCP-Protokoll mit einer Client-Server-Verbindung auf die Refbox zu. Die Roboter kommunizieren über das UDP-Protokoll mit einer p2p-Verbindung mit der Refbox.  

Die Nachrichten werden mit der Google Protobuf Bibliothek erstellt und verschlüsselt. Sie ist einfach in der Anwendung, ist erweiterbar und weitgehend kompatibel mit dem Austausch von Datenstrukturen. Nachrichten werden mit einem schlanken Framing-Protokoll übertragen.  

Im folgenden werden wir kurz eine Überischt von Protobuf geben und aufzeugen wie die Nachrichten definiert sind. Danach stellen wir das Framing-Protokoll vor und zeigen wie e verwendet wird, um Nachrichten zu übermitteln. Anschliessend beschreiben wir die grundlegenden Kommunikationsarten über Stream und Broadcast und schlussendlich noch eine Übersicht und ein Beispiel für den Gebrauch der Protobuf_Comm-Bibliothek, welche ein Teil der Refbox ist.
## <a name="SM1.1">Protobuf</a>
Protobuf bietet eine Beschreibungssprache, um Datenaustauschformate zu definieren, welche sehr effizient ver- und entschlüsselt werden können. Diese Formate sind erweiterbar und unterstützen, grundlegende Datentypen, Verschachtelungen, Wiederverwendung von Strukturen, effiziente Serialisierung und Deserialisierung, Listen mit variabler Länge und ein Kompiler, um Code für C++, Java oder Python zu generieren, für den Zugriff auf die Daten. In diesem Dokument geben wir nur eine sehr kurze Einführung und verweisen auf die Protobuf-Website für detaillierte Informationen.  

Datenstrukturen sind als nachrichtenenthaltende Felder definiert, so ähnlich wie die Datenstrukturen von C++. Jedes Feld hat eie Regel (erforderlich, optional oder mehrmalig), ein Typ, ein Namen und eine einmalige Kennzeichennummer. Die Regel definiert ob das Feld muss oder kann vorhanden sein oder ob es keinen, einen, oder mehrere Werte vom gegeben Typ haben kann. Der Typ kann entweder eine Anzahl von grundlegenden Typen oder ein anderer Nachrichtentyp sein. Das Kennzeichen muss mit der Nachricht übereinstimmen. Sie werden verwendet, um die Felder während der Deserialisierung zu identifizieren.  

Strukturen von anderen Files können verwendet werden, indem sie importiert werden. Als Beispiel kann das BeaconSignal.proto angesehe werden, welches in Abschnitt 3 als Beispiel vorliegt. Nach der Definition der Nachrichten in Proto-Files, müssen diese kompiliert werden, um den aktuellen Code zu generieren, um die Datenstrukturen verwenden zu können. Protobuf bietet support für C++, Java und Python. Für andere Sprachen existieren Programme von Dritten. Der Code muss dann in eine Bibliothek oder in deine Anwendung kompiliert werden.
## <a name="SM1.2">Framing-Protokoll</a>
Wenn die Protobuf-Nachrichten einmal serialisiert wurden, erhalten sie keine Informationen mehr über den enthaltenen Typ oder die länge der Nachricht. Um konfigurierbare Verschlüsselungsmethoden zu verwenden, benötigen wir den verwendetet Schlüssel. Um dies über das Netzwerk zu übermitteln ist das Framing-Protokoll erforderlich. Unser Protokoll besteht aus zwei Teilen, zum Einen aus einem Protokoll-Frame und zum Anderen ein Nachrichtenkopf, rechts im Bild als C-Struktur dargestellt. Später werden wir detaillierter den Nachrichtenkopf beschreiben und zeigen wie die Nachrichten gestaltet werden, hier zeigen wir erst nur eine kleine Übersicht. Das erste ist eine Struktur die Protokollinformationen beinhaltet, wie Version, Verschlüsselungsschlüssel und die Grösse der Nutzdaten. Das Zweite ist der Nachrichtenkopf der enthält die Protobuf-Nachricht-Komponenten und den Typ. Der Type erlaubt die Übertragung von beliebigen Nachrichten über die gleiche Verbindung. Jede Nachricht die über das Netzwerk gesendet wird enthält am Anfang einen solchen Nachrichtenkopf. Nachdem die Framekopfzeile gelesen wurde, muss der Empfänger so viele Bytes lesen, wie in der Nutzdatengrösse angegeben ist und falls die Nachricht verschlüsselt ist muss er auch noch die Grösse des IV-Kopfes (Initialization Vector) lesen, da der Schlüssel den VI benötigt.

Die Nachricht muss im 4-Byte-Muster liegen, wenn beispielsweise die Grösse der Framekopfzeilennachrichtenstruktur exakt 8 Bytes ergibt, wenn es über das Netzwerk gesendet wird, wird der Nachrichtenkopf exakt 4 Bytes gross. Alle enthaltene Zahlen müssen als 8 bit (uint8_t), 16 bit (uint16_t) bzw. 32 bit (uint32_t) vorzeichenlose Ganzzahlen umgewandelt werden.

Wenn eine Nachricht über das Netzwerk gesendet wird, wird zuerst die Protobuf-Nachricht serialisiert (zum bestimmen der Nutzdatengrössse). Danach wird der Frame und der Nachrichtenkopf vorbereitet mit der dazugehörigen Komponenten-ID, dem Nachrichtentyp und die Nutzdatengrösse, wie vorher festgelegt. Danach wird die Framekopfzeile gesendet, möglicherweise gefolgt von einer Verschlüsselung IV, dann folgt der Nachrichtenkopf und die serialisierte Nachricht.  

Beachte dass, für die UDP-Pakete, die Daten in einen einzigen gemeinsamen Puffer serialisiert werden müssen. Sonst kann der Netzwerkstapel des Betriebssystems die Übertragung in mehrere UDP-Nachrichten unterteilen. Das ist ungültig und kann auf der anderen Seite nicht entschlüsselt werden (UDP unterstützt nicht den Empfang in der korrekten Reihenfolge und kann die Packete nicht verknüpfen).
Wir werden nun den Frame und den Nachrichtenkopf im Deatil beschreiben und gbene ein paar Beispiele für verschlüsselte und unverschlüsselte Nachrichten.
### <a name="SM1.2.1">Frame-Kopfzeilenprotokoll</a>
**Protokollversion:** Die Verison vom Protokoll wird benötigt. Im Moment ist es die Version 2.  
**Schlüssel:** Die Schlüsselfolge wird benötigt. Die zulässigen Werte stehen in der folgenden Liste.  

| Wert | Verschlüsselungsmethode |  
| -------- | -------- |  
| 0x00 | Keine Verschlüsselung |  
| 0x01 | AES 128 ECB |  
| 0x02 | AES 128 CBC (benötigt 16-Byte IV) |  
| 0x03 | AES 256 ECB |  
| 0x04 | AES 256 CBC (benötigt 16-Byte IV) |  
 
**Reserviert:**   
Diese Bits werden momentan nicht gebraucht und müssen auf null gesetzt werden.  
**Nutzdatengrösse:**   
Grösse in Bytes von den folgenden Nutzdaten. Dies enthalten den Nachrichtenkopf und die serialisierte Protobuf-Nachricht. Sie enthalten **nicht** den Verschlüsselungs-IV-Kopf (wird bei einem Schlüssel benötigt). Die Nutzdatengrösse muss in der Netzwerk-Byte-Reihenfolge sein (Big-Endian).   
### <a name="SM1.2.2">Nachrichtenkopf</a>
**Komponenten-ID:**  
Generelle ID, generelle Adresse von Nachrichten. Für Refbox-Nachrichten muss die ID auf 2000 gesetzt werden (wie sie in der Protobuf-Nachricht im COMP_ID-Feld von der CompType-Aufzählung codiert ist). Falls du das Refbox-Framing-Protokoll für deine eigenen Nachrichten verwenden willst, musst du eine andere ID, als die von der Refbox, nehmen. Die Komponenten-ID muss  in der Netzwerk-Byte-Reihenfolge sein (Big-Endian).   
 
**Nachrichtentyp:**  
Nummerische Nachrichten-IDs von speziellen Nachrichten sind serialisiert in den Nutzdaten. Die ID muss sicher im MSG_TYPE-Feld von der CompType-Aufzählung codiert sein. Der Nachrichtentyp ist speziell für diese Komponenten-ID da. Eine Nachricht vom gleichen Nachrichtentyp kann unterschiedliche Komponenten-IDs habe, welche nicht verwandt sind. Der Nachrichtentyp muss in der Netzwerk-Byte-Reihenfolge sein (Big-Endian).   
### <a name="SM1.2.3">Unverschlüsselte Nachrichten</a>
Im Bild 1 siehst du den Byte-Aufbau für ein unverschlüsseltes Datenpaket. Jede Zeile repräsentiert 4 Datenbytes. Die Protokoll-Puffer-Nachricht ist einfach der Puffer der gemacht wird beim bevorstehenden Serialisieren der Nachricht. Die Komponenten-ID und der Nachrichtentyp muss speziell bei einer CompType-Aufzählung  in den Nachrichtendefinitionen gesetzt werden, z. B. 2000 und 1 für das Beacon Signal.
### <a name="SM1.2.4">Verschlüsselte Nachrichten</a>
Im Bild 2 siehst du den Byte-Aufbau für ein verschlüsseltes Datenpaket. Es ist ähnlich aufgebaut wie das unverschlüsselte Packet mit wesentlichen Unterschieden. Erstens ist zusätzlich zwischen dem Frame und dem Nachrichtenkopf der IV platziert und zweitens sind der Nachrichtenkopf und die Protobuf-Nutzdaten verschlüsselt.
### <a name="SM1.2.5">Verschlüsselungsmethoden</a>
Die Verschlüsselung ist momentan eingebaut mit der Absicht, einen einfachen Schutz anzubieten, besonders um zu verhindern, dass versehentlich Nachrichten an das falsche Team übertragen werden. Beispielsweise verlangen wir nicht einen Zeitstempel innerhalb dem verschlüsselten Teil, welcher gegen die wiederholenden Attacken unterstützen würde. Diese ist da, um den Bedarf für eine Zeitsynchronisation zwischen den Robotern und der Refbox, zu vermeiden. Dies könnte zu einem späteren Zeitpunkt hinzugefügt werden.  

Das Framing-Protokoll unterstützt pro Nachricht Verschlüsselungen basierend auf einem symmetrischen Ziffernblock. Derzeit basieren die unterstützten Verschlüsselungsmethoden auf dem AES-Algorithmus entweder mit einem 128 oder 256-bit Schlüssel, entweder in einem Elektronischen Codebuch (ECB Electronic Code Book) oder in einem Ziffernblock-Verbindungsmodus (CBC Cipher Block Chaining). Beim Wettkampf wird die Refbox den AES-128-CBC-Modus benützen. Das heisst das dann dort ein 16-Byte Initialisationsvektor (IV) ist, welcher benutzt wird, um verschiedene verschlüsselte Nachrichten für den selben Eingang zu generieren (so lange wie unterschiedliche IVs unterstützt werden).   

Die Protobuf-Bibliothek behandelt dies einfach für dich. Alles was du tun musst ist, die Verschlüsselung auf dem Teamkanal Broadcast-Peer aktivieren. Falls du deine eigene Implementation erstellen möchtest, nimm bitte noch Bezug auf die Klassen BufferEncryptor und BufferDecryptor in der Protobuf_comm-Bibliothek. Der IV muss in jeder übermittelten Nachricht unterschiedlich sein. 
## <a name="SM1.3">Kommunikationsmethoden</a>
Die Refbox verwendet zwei Kommunikationsmethoden. Ein TCP-Verbindungsbasiertes Streamingprotokoll wird verwendet für die Kommunikation zwischen der Refbox und den Controllern, wie das Shell oder GUI. Teams können diese Methode nicht verwenden, um die Refbox zu kontaktieren. Für solche Kommunikationen arbeitet ein UDP-basiertes Broadcastprotokoll.  

Da ja das Wi-Fi grundsätzlich unzuverlässig ist, besonders während einem RoboCup-Wettkampf, können die Verbindungen jederzeit abbrechen. Insbesondere in einem betriebsamen Wireless-Netzwerk kann ein TCP-Handshake die Geschwindigkeit verlangsamen oder sogar zuverlässige Kommunikationen fehlschlagen und sind schuld für die Häufung Wiederholübertragungen. Deshalb wurde für die Kommunikation mit den Robotern das UDP-Protokoll gewählt. Derzeit brauchen wir Broadcasting um die Informationen an alle Roboter gleichzeititg zu senden. In Zukunft könnte dies zu Multicast erweitert werden.   

Um die Stream-Kommunikation zu installieren, empfehlen wir  sie so zu installieren, dass immer zuerst der Frame Header gelesen wird und dann erst die Nutzdaten, abhängig von der im Header gegebenen Grösse.  

Broadcast ist zusätzlich in drei Kommunikationsgruppen unterteilt: öffentlich,  Team Cyan und Team Magenta. Grundsätzlich sollten die Teams immer auf ihrem privaten Teamkanal senden und  beiden zuhören, dem privaten und dem öffentlichen Kanal. Die Refbox sendet das BeaconSignal und den Spielzustand auf dem öffentlichen Kanal, es ist das gleiche für beide Teams. Andere Nachrichten wie Bestellinformationen oder Explorationsinformationen werden auf dem Teamkanal gesendet. Die exakte Aufgabe ist in der Beschreibung der Nachricht festgelegt.  

Stelle bei der Broadcast-Kommunikation sicher, dass eine komplette Buffer-Nachricht inklusive dem Frame Header und der serialisierten Nachricht gebildet wird und sende alles auf einmal, um eine Zerlegung zu vermeiden. Gestalte beim Lesen einen ausreichend grossen Buffer, um das ganze Packet auf einmal zu lesen. Danach den Frame Header vom Buffer lesen und die Nachricht entserialisieren. 
### <a name="SM1.3.1">Kommunikationsgruppen</a>
Die Refbox unterschiedet zwischen vier Kommunikationsgruppen. Diese sind im Bild 3 dargestellt. Jedes Team braucht zwei zu öffnen und benötigt während dem Spiel nur zwei Broadcast-Peer-Kommunikationskanäle.  

**Stream**  
Die Refbox akzeptiert Stream-Client-Verbindungen auf Port TCP 4444. Während dem Wettkampf werden höchstwahrscheinlich nur Verbindungen von lokalen oder ausgewählten Hosts zugelassen. Weder ein Roboter noch ein Gerät von einem anderen Team können das Streamprotokoll zum Kommunizieren mit der Refbox benützen.   

**Öffentlich**  
Der öffentliche Broadcast-Kanal ist auf Port UDP 4444 eingerichtet. Teams können auf diesem Kanal nur zuhören, aber nicht senden.   

**Teamkanal**  
Es sind zwei Teamkanäle auf Port UDP 4441 (Cyan) und 4441 (Magenta). Jeder Kanal wird mit einem teamspezifischen Verschlüsselungsschlüssel, den das Team, vor dem Wettkampf, vorbereitet und mitbringt, verschlüsselt (und könnte später noch geändert werden, sollte Bedarf bestehen). Es wird gebraucht für die private Kommunikation zwischen den Teams und der Refbox.  
### <a name="SM1.3.2">Verschlüsselungsaufbau</a>
Die Verschlüsselung auf dem Teamkanal sollte nur konfiguriert werden, wenn die Refbox dem jeweiligen Teamnamen eine der zwei Farben ankündigt.  Teams können niemals Nachrichten über den privaten Teamkanal senden, wenn er für ein anderes Team als das Eigene konfiguriert ist.  
Der empfohlene Durchlauf für die Verschlüsselung aufzubauen ist:
- Auf dem öffentlichen Kanal auf Spielstatus-Nachrichten zu hören.
- Falls der eigene Teamname, als Cyan oder Magenta-Teamname empfangen wird, die Verschlüsselung auf dem entsprechenden Kanal aufbauen.
- Nachrichten auf dem Teamkanal senden, niemals eine Nachricht auf einem Kanal, von einem anderen Team, senden. 

## <a name="SM1.4">Beispiel für den Gebrauch der Protobuf_Comm-Bibliothek</a>
Die Protobuf_Comm-Bibliothek unterstützt die Implementierung von Netzwerkkommunikation mit Protobuf-Nachirchten brauchen das Framing-Protokoll beschrieben mehr als für beide Kommunikationsmethoden. Es ist abrufbar als Teil vom Refbox-Quellcode im Verzeichnis ***src/libs/protobuf_comm***. Die Implementation braucht "Boost Asio" für die asynchrone I/O implementierung und "Boost Signals2", um Ereignisse zu unterstützen, auf die dein Code verbinden kann. Die Protobuf_Comm-Bibliothek benötigt momentan ein Compiler, welcher Code gemäss dem C+ +11-Standard akzeptiert, z. B. GCC 4.6 oder höher.  

Die Bibliothek hat hauptsächlich drei zusammenwirkende Klassen, die du benutzen kannst oder auch nicht. Zuerst wird eine ProtobufStreamClient-Klasse implementiert mit einer TCP-Sockelverbindung, welche das Framing-Protokoll braucht, um Nachrichten vom und zum ProtobufStreamServer, der auf der Refbox läuft, zu empfangen und übertragen. Zweitens der ProtobufBroadcastPeer implementiert eine p2p-Verbindung über UDP mit dem Framing-Protokoll. Zum Schluss ist der MessageRegister beschäftigt bei beiden Klassen mit dem Registrieren von Nachrichten, auf die du reagieren möchtest. Nachrichtentypen müssen mit dem MessageRegister registriert sein, so dass der Client oder Peer wissen kann, wie die einkommenden Nachrichten deserialisiert werden sollen. Nachrichten mit einem unbekannten Typ werden ignoriert.   

Die Bibliothek benutzt den Signal-Slot-Event-Pattern, um deinem Code Events wie verbunden sein, getrennt sein oder angekommene Nachrichten anzukündigen. Dies ist am Anfang von BoostSingals2 aufgebaut. Beachte dass dies nicht kompatibel ist mit Boost.Signals. Signals2 wurde gewählt, weil es eine erhöhte Thread-Sicherheit unterstützt. Der ProtobufStreamClient and der ProtobufBroadcastPeer starten ein mitlaufender Thread, um ankommende Daten zu verarbeiten. Deshalb, wenn ein Signal ausgegeben wurde, geschieht es im Rahmen vom empfangenden Thread. Für den Code ist dies nicht Thread-sicher oder das erwartet Events nur von einem bestimmten Thread (z. B. GUI-Appliaktionen mit Gtkmm oder ebenso Texteingaben mit ncurses) du brauchst zum implementieren einen Dispatch-Pattern der wird ausgeben einen Event der ist untersucht in diesem Main-Thread.   

In Bild 4 siehst du den Code als Beispiel wie die Peer-Kommunikation zu verwenden ist. Du findest den Code im Verzeichnis ***src/examples*** im Installationsort der Refbox. du kannst den Code anpasssen und in dein bestehendes System integrieren. Der ganze Quellcode kann zum Testen in einem Stand-alone-Programm kompiliert werden. Allerdings solltest du den Code mit deinem eigenen Main Loop integrieren und nicht den Abreisszettel vom Beispiel kopieren.   

Im Konstruktor von der Klasse "ExamplePeer" ist der Peer erstellt (Linie 13 und 14), welcher auch einen neuen MessageRegister erstellt, der gebraucht wird. Bei Linie 13 und 14 der MessageRegister vom Peer wird erneuert und ein SingleMessageType wird registriert. Beachte dass keine Komponenten-ID oder Nachrichtentyp  unterstützt werden. Sie werden vom CompType Zahlenfeld innerhalb von den Nachrichtenspezifikationen abgerufen (vgl. Abschnitt 3).
In Zeile 16-20 sind die Signale vom Peer verbunden mit den Methoden von der Klasse "ExamplePeer". Die Events können abgerufen werden, sobald  das Signal verbunden ist. Also stelle sicher, dass von den benötigten Ressourcen alle Initialisationen abgeschlossen oder grantiert sind, wenn die Signale verbunden werden. Die Methoden ***peer_error*** (Linie 30ff.) und ***peer_msg*** im "ExamplePeer" werden aufgerufen, wenn eine Nachricht nicht emfangen werden konnte resp. der Empfang gelungen ist. Weil die UDP-Kommunikation kontaktlos funktioniert, gibt es keine Signale über verbunden oder nicht verbunden. Um zu detektieren ob die Refbox erreichbar ist, muss auf die einkommenden BeaconSignal-Nachrichten gehört werden. In der Methode ***peer_msg*** gibt es zwei Wege um zu entscheiden welche Nachricht empfangen wurde. Entweder mit der Komponenten-ID und dem Nachrichtentypnummer (immer beide) oder mit C++ Run-time Type Information (RTTI). Das Letztere wird bevorzugt und wird im Beispiel gezeigt. Es garantiert eine starke Typisierung. Wie immer sollte nicht vergessen werden, die Ressourcen vom Peer freizumachen, indem es gelöscht wird, wenn es nicht länger benötigt wird (Destruktor Linie 24ff.).  

Im Konstruktor der Klasse ExampleClient wird der Benutzer esrtellt (Linie 12). Bei Linie 14-15 wird der MessageRegister, vom Benutzer, erneuert und SingleMessageType wird registriert. Beachte dass keine Komponenten-ID oder Nachrichtentyp unterstützt wird. Sie werden vom CompType-Zahlenfeld innerhalb der Nachrichtenspezifikationen abgerufen (vgl. Abschnitt 3). Bei Linie 16-23 werden die Signal vom Benutzer verbunden mit der Methode von der Klasse ExampleClient. Die Events können ausgegeben werden sobald der Benutzer verbunden ist. Die Methode ***async_connenct*** vom Benutzer wird die Verbindung zum Server ansteuern, wird sie aber nicht blockieren. Stelle sicher, dass von den benötigten Ressourcen alle Initialisationen abgeschlossen oder grantiert sind, wenn der Benutzer verbunden wird. Sobald die Verbindung steht, kann das ***connected*** Signal ausgegeben werden und dadurch auch die Methode ***client_connected*** von ExampleClient aufgerufen werden (Linie 35ff.) Zugleich sollte, wenn die Verbindung abbricht, die Methode ***client_disconnected*** aufgerufen werden, mit einer Errornummer, welche auf den Grund des Fehlers hinweist. In der Methode ***client_msg*** gibt es zwei Wege, um zu entscheiden, welche Nachricht empfangen wurde. Entweder mit der Komponenten-ID und dem Nachrichtentypnummer (immer beide) oder mit C++ Run-time Type Information (RTTI). Das Letztere wird bevorzugt und wird im Beispiel gezeigt. Es garantiert eine starke Typisierung. Wie immer sollte nicht vergessen werden, die Ressourcen vom Peer freizumachen, indem es gelöscht wird, wenn es nicht länger benötigt wird (Destruktor Linie 24ff.).

# <a name="SM2.0">Messages</a>
In diesem Abschnitt beschreiben wir die aktuellen Nachrichten, welche für die Kommunikation verwendet werden. Sie werden mit der oben beschriebenen Infrastruktur, in Übereinstimmung mit den Regeln und den im LLSFRuleBook beschriebenen Regelungen, übertragen.   

Nachrichten benötigen eine Komponenten-ID und einen Nachrichtentyp.  Die Tupel (geordnete Wertesammlung (eindimensionale Arrays)) muss zwischen allen Nachrichten einmalig sein. Die Refbox benutzt die Komponenten-ID 2000 für alle ihre Nachrichten. Die Nachrichten sind ein einer Datei, wenn sie direkt verwandt sind. Innerhalb einer Datei ist ein Block von zehn  Nachrichtentyp-IDs definiert (mit den hauptsächlichen Nachrichten BeaconSignal, AttentionMessage und VersionInfo sind eine Ausnahme).   

Die Nachrichtentypen sind verschlüsselt in den Nachrichten-Protodateien als ein CompType Sub-Type-Aufzählung pro Nachricht. Der CompType muss immer in der gleichen Form sein, mit einer COMP_ID und einem MSG_TYPE. Die COMP_ID ist der Komponenten-ID zugeordnet, z. B. 2000 für die Refbox. Der MSSG_TYPE ist der Typenidentifikationsnummer von einer bestimmten Nachrichten zugeordnet. Sie müssen zwischen allen LLSF-Refbox-Nachrichten einmalig sein. Eine Nachrichtentypnummer kann nicht mehr verwendet werden, sobald ein Nachrichtentyp entfernt wurde, es ist nicht zu verwechseln, dass ältere Peers den alten Nachrichtentyp erwarten.  

Im folgenden zeigen wir die Spezifiaktionen von Protobuf und eine Beschreibung von allen Nachrichtentypen, welche momentan für die LLSF-Refbox-Kommunikation verwendet werden. Das Feld "Via" beschreibt welcher Kommunikationskanal für die Übertragung verwendet wird, es kann entweder öffentlicher Broadcast (P), privater Teambroadcast (T) oder Stream (S) oder eine Kombination davon sein. Viele Nachrichten werden mit einer bestimmten Periode gesendet. Diese sind in Sekunden, zwischen zwei gesendeten Nachrichten, angegeben oder es steht Event, wenn sie nur bei bestimmten Events gesendet wird.  Einige Broadcast-Nachrichten haben einen Burst-Mode, um einige Packete mit dem gleichen Inhalt in einer kurzen Reihenfolge zu versenden, um die Chance zu erhöhen, die anderen Peers zu erreichen. Die Felder "Sent by" und "Sent to" zeigen den Sender und den Empfänger der Nachricht. Ein Controller ist das GUI oder Shell der Refbox zum mit der Refbox zu kommunizieren, es ist nicht ein Gerät eines Teams. Alle Proto-Dateien sind im Verzeichnis ***src/msgs*** vom Refbox-Quellcode. Du kannst diese Dateien frei kopieren und in deinen eigenen Code kopieren, in diesem Fall stelle aber sicher, dass du auf Updates achtest und diese integrierst.  
Die Absicht istm, die Änderungen möglichst gering zu halten, besonders wenn ein Wettkampf bevorsteht. Aber in manchen Situationen kann es nötig sein, z. B. um Probleme zu beheben.

### <a name="SM2.1">Attention Messages</a>
**File:** *AttentionMessage.proto*
>Wird im Stream gesendet. Bei jedem Event. Die Nachricht wird von der Refbox an den Controller versendet.

Wenn etwas unvorhergesehenes passiert, was eine menschliche Interaktion erfordert, wird diese "Meldung zur Aufmerksamkeit" an den Controller gesendet. Das kann zum Beispiel sein, wenn ein zu  spät bestellter Puck gesetzt werden muss oder falls die Kommunikation zu einem Roboter verloren ging.
### <a name="SM2.2">Beacon Signal</a>
**File:** *BeaconSignal.proto*
>Wird über den offenen und den privaten Kanal gesendet. Periodisch alle Sekunde. Das Signal wird von den Robotern und der Refbox an alle gesendet.

Das Beaconsignal wird periodisch gesendet, um die Roboter und die Refbox im Netzwerk zu detektieren.  Wenn ein Roboter erstmals detektiert wird, wird der Zeitwert verwendet um den Zeitversatz zu vergleichen. Die Netzwerkverzögerungen werden nicht in die Berechnungen mitgenommen. Der Controller kann eine Warnung ausgeben, wenn der Zeitversatz zu lang ist. Der Teamname und der Robotername werden benötigt, um mögliche Verbindungsprobleme zu diagnostizieren. Die Refbox wird diese Felder jeweils auf "LLSF" und "RefBox" setzen. Die Roboter müssen ausserdem die Teamfarbe setzen, einzig die Refbox muss diese nicht setzen.  

Die Nachrichten der Refbox werden auf dem öffentlichen Kanal gesendet. Die Roboter müssen den privaten Kanal nutzen.  

Kommt von einem Roboter kein Signal, wird er nach 5 Sekunden als verloren betrachtet. Nach 30 Sekunden gilt er als verloren.  

Wir wünschten uns, dass die Roboter ihre Position auf dem Spielfeld preisgeben, um das Spiel darzustellen. Das würde nicht nur dem Schiedsrichter helfen, sondern würde das Spiel auch interessanter für die Zuschauer machen.
### <a name="SM2.3">Versionsinfo</a>
**File:** *VersionInfo.proto*
>Wird über den Stream und den öffentlichen Kanal gesendet. Bei einem Event. Die Nachricht wird von der Refbox an jeden Teilnehmer gesendet.

Die Versionsinfo wird an jeden neuen verbundenen Stream-Client, als erste Nachricht geschickt. Zusätzlich wird jedes Mal, wenn ein neuer Peer im Netzwerk erkannt wird, die Versionsinfo 10 Mal mit einer Periode von einer halben Sekunde geschickt. Die Informationen können verwendet werden, um die Kompatibilität sicherzustellen und warnt nach zukünftigen Upgrades der Refbox.
### <a name="SM2.4">Zeit</a>
**File:** *Time.proto*
>Dieses Konstrukt wird als Slave-Nachricht von anderen Nachrichten verwendet. Es wird nie alleine geschickt. 

Es beinhaltet entweder einen Zeitpunkt oder eine Zeitdauer. Was gesendet wird hängt von der Master-Nachricht ab.  

Ein Zeitpunkt ist gegeben entsprechend der Unix Zeitzone in UTC-Zeit. Für ein Beispiel kann die clock_gettime() POSIX API aufgerufen werden oder die Methode posix_time::universal_time() von Boost.  

Eine Zeitdauer gibt einfach die Anzahl Sekunden seit dem Start und die Anzahl der Nanosekunden seit dem Start der Sekunde.
### <a name="SM2.5">Position</a>
**File:** *Pose2D.proto*
>Dieses Konstrukt wird als Slave-Nachricht von anderen Nachrichten verwendet. Es wird nie alleine geschickt. 

Es beschreibt die Position und die Orientierung des Roboters auf dem Spielfeld. Der Koordinaten-Bezugsrahmen ist im Rule Book beschrieben.
### <a name="SM2.6">Team</a>
**File:** *Team.proto*
>Dieses Konstrukt wird als Slave-Nachricht von anderen Nachrichten verwendet. Es wird nie alleine geschickt. 

Es beinhaltet die Teamfarbe, welche entweder CYAN oder MAGENTA sein kann.
### <a name="SM2.7">Explorationinfo</a>
**File:** *ExplorationInfo.proto*
>Wird über den öffentlichen Kanal gesendet. Periodisch all Sekunde. Die Nachricht wird von der Refbox an die Roboter versendet.

Diese Nachricht wird während der Explorationsphase periodisch gesendet. Es kündigt die Zuordnung von Typnamen zu den Lichtsignalen und die Maschinennamen zu ihren Positionen im Spielfeld an die Roboter an. In der Signalliste wird ein Eintrag pro Maschine stehen. Die Lampenliste in der Slave-Nachricht *ExlporationSignal* hat einen Eintrag pro Lichtfarbe, selbst für Lampen die ausgeschaltet sind. Das Maschinenfeld hat zur Identifikation einen Eintrag pro Maschine. Die Maschinen haben einen Namen zugewiesen, der auf die Position im Spielfeld hindeutet. Bemerke das diese Namen für die Maschinen während dem Spiel anders heissen können, als im RuleBook beschrieben.

Beachte die Teamfarbe der Maschine. Es wird nur die Maschinen gezählt, welche mit der Teamfarbe übereinstimmen. 

Falls die Möglichkeit besteht, dass ein oder mehrere Roboter die Nachricht nicht erhalten, wird empfohlen das Spiel für einige Zeit in den Pausen-Modus zu setzen. Das Senden der Nachricht wird dabei fortgesetzt, sodass der Roboter die Möglichkeit hat wieder aufzuschliessen, ohne das Spiel zu gefährden.
### <a name="SM2.8">Spielinfo</a>
**File:** *GameInfo.proto*
>Wird über den Stream gesendet. Beim Start. Die Nachricht wird von der Refbox an den Controller gesendet.

Die Nachricht beinhaltet zusätzliche Informationen über das Spiel. Die Nachricht wird gesendet, wenn zum ersten Mal die Verbindung von der Refbox zum Controller hergestellt wird. Derzeit beinhaltet es eine Liste mit den Teams, welche als Spielteilnehmer gesetzt werden können.
### <a name="SM2.9">Spielstatus</a>
**File:** *GameState.proto*
>Wird über den Stream und den öffnetlichen Kanal gesendet. Periodisch all Sekunde. Die Nachricht wird von der Refbox an alle Teilnehmer gesendet.

Die Nachricht wird periodisch über p2p an alle Roboter gesendet, sowie über eine Client-Server-Verbindung zu den verbundenen Controllern. Die Spielzeit wird in der Explorationsphase und in der Produktionsphase neu gestartet. Die Explorationsphase dauert 3 Minuten und die Produktionsphase dauert 15 Minuten. 

In den Phasen PRE_GAME und der POST_GAME, sowie in allen anderen Zuständen, ausser RUNNING, muss der Roboter sofort und die ganze Zeit still stehen. 

Die Nachrichten *SetGameState* und die *SetGamePhase*  können benutzt werden, um jeweils eine neue Spielphase oder einen neuen Spielzustand anzufordern. Dies kann aber nur durch den Controller geschickt werden. Aber Achtung, das Setzen einer neuen Phase löst einen Neustart von dieser Phase aus. Um ein Spiel zu unterbrechen wird der Spielzustand auf PAUSE gesetzt, eine Spielphase sollte nur abgeändert werden, wenn man die Änderungen unabänderlich machen möchte. Es ist Verboten dieses Signal von einem Roboter aus zu senden. Dies wird von der Refbox detektiert und als Betrugsversuch geandet.
### <a name="SM2.10">Maschineninfo</a>
**File:** *MachineInfo.proto*
>Wird über den Stream und den privaten Kanal gesendet. Periodisch all Viertelsekunde. Die Nachricht wird von der Refbox an alle Teilnehmer gesendet.

Das Maschineninfo-Signal wird periodisch von der Refbox an die Controller und in der Produktionsphase auch an die Roboter gesendet. Das Signal für die Controller enthält statische und dynamische Informationen über alle Maschinen.  

**Statische Informationen:**  
Eingänge, Ausgänge, Namen, Typ, Position  
**Dynamische Informationen:**   
Pucks die in der Maschine geladen sind, Pucks die unter dem RFID-Sensor platziert sind oder ob die Maschine während der Exploratosnphase korrekt erfasst wurde   

Die Refbox kann nur Lichter erkennen, welche leuchten oder blinken. Lichtfarben die nicht erwähnt sind, werden als augeschaltet betrachtet. Es kann verwendet werden, um optisch den aktuellen Zustand der Maschine abzugleichen. Das Signal wird all Viertelsekunde gesendet.  

Das Signal für die Roboter beinhaltet nur den Namen, Typ, Eingangs-Puck-Typ, Ausgangs-Puck-Typ und Position. Es wird nur während der Produktionsphase über den privaten Kanal gesendet. Zu Beginn der Produktionsphase wird das Signal während 15 Sekunde, all halbe Sekunde gesendet. Nach den 15 Sekunden wird das Signal alle 2 Sekunden gesendet.

In beiden Fällen ist die Maschineninfo und Typen von Maschinennachrichten mit der Teamfarbe versehen. Beim Zweitgenannten ist die Teamfarbe immer gesetzt. Bei den Maschineninfos unterscheidet sich das Verhalten zwischen Stream und Broadcast. Bei Nachrichten über den Stream wird häufig die Maschineninfonachricht mit allen Maschinen, von beiden Teams, gesendet. Beim Broadcasting werden zwei Nachrichten gesendet, eine für je ein Team. In dieser Nachricht wird die Teamfarbe gesetzt und nur Maschinen mit der gleichen Farbe bekommen diese Nachricht.

Während dem Spiel sollte der Schiedrichter an der Refbox besonders auf andere Controller achten, die angeschlossen sind (Das wird im Logfenster angezeigt). Kein Teamcomputer oder Roboter ist es erlaubt eine Verbindung zur Refbox aufzubauen., weil besonders die Maschinenstatusinformationen ein Betrügen ermöglichen.
### <a name="SM2.11">Maschinenkommandos</a>
**File:** *MachineCommands.proto*
>Wird über den Stream gesendet. Bei einem Event. Die Nachricht wird vom Controller an die Refbox gesendet.

Diese Protobuf-Datei enthält Nachrichten für spezielle Anweisungen an die Refbox. Zum Beispiel ein Puck in der Maschine zu platzieren bzw. zu laden oder einen zu entfernen. Dieses Kommando kann also genutzt werden, um ein Spiel zu simulieren, das als Trainingsrefbox dient (ohne eine lauffähige PLC).
### <a name="SM2.12">Maschinenbericht</a>
**File:** *MachineReport.proto*
>Wird über den privaten Kanal gesendet. Periodisch alle zwei Sekunden. Die Nachricht wird von den Robotern an die Refbox gesendet.

Während der Explorationsphase melden die Roboter die entdeckten Maschinen mit dem Maschinenbericht, der den Namen und den Typ enthält. In einer Nachricht können eine oder mehrere Maschinen gemeldet werden. Wir empfehlen, dass immer alle entdeckten Maschinen im Report gesendet werden. Wenn einmal Packete verloren gehen, kann man so sichergehen, dass schlussendlich alle Maschinen an die Refbox gemeldet wurden. Die Nachrichten sollten periodisch gesendet werden, so als Richtwert sind 2 Sekunden ideal.

Beachte dass für jede Maschine nur der erste empfangene Bericht akzeptiert wird und die Punkte gemäss dem Regelbuch und der Genauigkeit gegeben werden. Es is nicht möglich eine falschen, abgegebenen Bericht noch zu korrigieren. Jede nachträgliche Wiederholung wird einfach ignoriert. Ebenfalls sollte sichergestellt werden, dass die gesendeten Berichte auch die richtige Teamfarbe enthalten, sonst werden sie ebenso ignoriert. Das Senden von Maschinenberichten von Maschinen, die nicht zum Team gehören, mit der anderen Teamfarbe ist ein Verstoss.

Falls mehrere Roboter im Feld stehen, ist es nicht nötig die Berichte zu einem Bericht zusammenzufassen. Stattdessen kann jeder Roboter unabhängig seine Meldungen direkt zur Refbox schicken. Wie auch immer es gemacht wird, sollte wieder beachtet werden, dass nur der erste Bericht über jede einzelne Maschine berücksichtigt wird.
### <a name="SM2.13">Bestellung</a>
**File:** *OrderInfo.proto*
>Wird über den Stream und den privaten Kanal gesendet. Periodisch alle 5 Sekunden. Die Nachricht wird von der Refbox an alle Teilnehmer gesendet.

Während der Produktionsphase sendet die Refbox periodisch die aktuelle Bestellung an alle Roboter und Controller. Beachte das die Liste mit den Bestellungen in der Nachricht geändert werden. Falls eine Bestellung als verspätet markiert wird, erscheinen neue Bestellungen in der Nachricht. Zudem sollte die Lieferfrist der Bestellung beachtet werden. In der Nachricht werden wahrscheinlich meistens Bestellungen mit einer Lieferfrist aufgegeben, während bereits wieder Bestellungen kommen oder gekommen sind.

In beiden Fällen ist die Bestellliste und Typen von Bestellungen mit der Teamfarbe versehen. Beim Zweitgenannten ist die Teamfarbe immer gesetzt. Bei den Bestellungen unterscheidet sich das Verhalten zwischen Stream und Broadcast. Bei Nachrichten über den Stream wird häufig die Bestellliste mit allen Bestellungen, von beiden Teams, gesendet. Beim Broadcasting werden zwei Nachrichten gesendet, eine für je ein Team. In dieser Nachricht wird die Teamfarbe gesetzt und nur Bestellungen mit der passenden Farbe werden miteinbezogen.

Wenn eine neue Bestellung eingeht, geht die Refbox in einen kurzzeitigen Explosionsmodus, für ein paar Sekunden. Während dieser Zeit, sendet die Refbox zehn Nachrichten mit einer Periode von einer halben Sekunde. Danach geht die Refbox wieder in die normale Periode von 5 Sekunden.
### <a name="SM2.14">Puckinfo</a>
**File:** *PuckInfo.proto*
>Wird über den Stream gesendet. Periodisch all Sekunde. Die Nachricht wird von der Refbox an den Controller gesendet.

Die Puckinfo wird von der Refbox periodisch an die angeschlossenen Controller gesendet. Sie enthält Statusinformationen über alle Pucks, die der Refbox bekannt sind. Das Refbox-GUI benötigt diese Informationen für ihre Puck-Anzeige. Jeder Puck hat eine einmalige ID und einen aktuellen Zustand.

Die Positionsinformationen sind freiwillig und werden momentan nicht unterstützt. Zukünftig könnten die Informationen durch ein kamerbasiertes Verfolgungssytem (OpenCV) gebraucht werden.
### <a name="SM2.15">Roboterinfo</a>
**File:** *RobotInfo.proto*
>Wird über den Stream und den öffentlichen Kanal gesendet. Periodisch all Sekunde. Die Nachricht wird von der Refbox an den Controller gesendet.

Die Roboterinfo wird von der Refbox periodisch an die angeschlossenen Controller gesendet. Sie enthält Informationen über alle Roboter, die der Refbox bekannt sind. Es wiederspiegelt die gesammelten Meinungen von den verarbeiteten Beacon-Signalen von den Robotern. Es enthält auch einen Hostnamen von wo das Beaconsignal empfangen wurde, um beispielsweise das Problem zu erkennen, wenn ein Roboter verloren ging.

Die Positionsinformationen sind freiwillig. Für die Teams die entscheiden die Informationen im BeaconSignal bereitzustellen, wird es für eine Visualisierung an den Controller geschickt.
### <a name="SM2.16">Roboterkommandos</a>
**File:** *RobotCommands.proto*
>Wird über den Stream gesendet. Bei einem Event. Die Nachricht wird vom Controller an die Refbox gesendet.

Kommandos die zu einem Roboter gehören können die Controller an die Refbox schicken. Momentan ist die einzige Möglichket mit dieser Nachircht den Instandhaltungszustand von einem bestimmten Roboter von einem bestimmten Team zu setzen.

----
Last edited by Florian Gehrig at 15. Juni 2015.  
