## Configuration of the Lancom Router

----
Autor: Florian Gehrig, Lukas Hofmann  
Klasse: HF2A  
Datum: 27. Mai 2015  
Version: 2.0  
Quellen: [EDV-Abkürzungen](http://www.edv-abkuerzungen.de/definition/erklaerung/DSLOL.html) | [LANCOM Knowledgebase](https://www2.lancom.de/kb.nsf/bf0ed2a4d2a4419ac125721b00471d85/8fe50847c2dd2e14c12573bf0048961c?OpenDocument)

----
- <a href="#SM1">Zugriff auf Router</a>
- <a href="#SM2">Default-Setup</a>
- <a href="#SM3">Setup-Assistent</a>
- <a href="#SM4">Gerät konfigurieren</a>
- <a href="#SM5">Änderungen während dem Cup</a>

----

>Arbeitsschritte die ausgeführt werden müssen, wenn der Lancom-Router auf die Werkseinstellungen zurückgesetzt wurde.  

### <a name="SM1">Zugriff auf Router</a>
PC-Interface konfigurieren  
IP-Adresse: ***172.23.56.253***  
Netzmaske: ***255.255.255.0***  
Im Browser die Adresse eingeben: ***172.23.56.254***    
Der Router startet mit dem *Default-Setup*.  
### <a name="SM2">Default-Setup</a>
1. Gerätename: ***LancomRobot***
2. Administrator: ***root***
3. Gerätepassswort: ***soliduscup15***
4. SNMP Read-Only Community: ***private***
5. DHCP-Betriebsart: ***Server***
6. IP-Adresse: ***172.26.0.1***
7. Netzmaske: ***255.255.0.0***

Nach dem Default-Setup im PC-Interface die IP ändern, das LANconfig-Programm öffnen und den Router suchen. Danach im Programm den Setup-Assistent aufrufen.
### <a name="SM3">Setup-Assistent</a>
1. Setup-Assistent für LancomRobot
2. Internet-Zugang einrichten
3. Eine neue Verbindung anlegen für IPv4
4. Mein Land ist nicht aufgeführt
5. Internet-Zugang über Plain Ethernet (IPoE)
6. Name der Verbindung: INTERNET
7. IP-Parameter automatisch vom DHCP-Server beziehen
8. Keine Verbindungsüberwachung verwenden

### <a name="SM4">Gerät konfigurieren</a>
![Configuration](https://gitlab.com/solidus/hefei/uploads/e063bf7dfbf355609e66a190435d10ae/Configuration.jpeg)
### <a name="SM5">Änderungen während dem Cup</a>
Bei einer Einstellung des Routers waren wir stets unsicher über die Auswirkungen auf das Netz. Es betrifft den Modus des DSLoL-Interfaces im Menü *Schnittstellen/WAN*. Der Modus vom DSLoL kann wahlweise zwischen Automatisch und Exklusiv umgeschaltet werden. DSLoL ist die Abkürzung für DSL over Lan. Damit kann auf einem LAN-Interface (LAN oder WLAN) ein WAN-Port eingerichtet werden. Im **Automatisch-Modus** werden alle PPPoE-Frames sowie alle Datenpakete, die zu einer über DSLoL-Interface aufgebauten Verbindung gehören (Konfiguriert in der IP-Parameter-Liste), über das DSLoL-Interface (WAN) weitergeleitet. Alle anderen Datenpakete werden als normale LAN- Pakete behandelt. Im **Exclusiv-Modus** wird das LAN-Interface ausschliesslich als WAN-Interface benutzt. Im Netz der BFH hatten wir das Problem, dass wenn der Automatisch-Modus aktiviert ist, der DCHP weitergeleitet wird. Das heisst, der Router fungierte als Switch und gab einfach die BFH-Adressen an die Clients weiter. Wir wollten aber ein eigenständiges Netz aufbauen, welches dem offiziellen Netz des Cups entspricht. Mit dem richtigen Adressbereich. Alsdann in den Exclusiv-Modus umgeschaltet wurde, hatten wir nur noch ein WAN-Interface und konnten unser Vorhaben umsetzen. 

Während dem RoboCup wird der Router an das Netz des Veranstalters gehängt. Diese erlauben kein und haben selber auch kein DHCP-Server. Am Anfang des Cups hatten wir Probleme mit der Verbindung zu Refbox. Wir konnten zwar Informationen erhalten, aber keine senden. Lukas erinnerte sich an das Problem mit der BFH. Nun waren wir am offiziellen Cup-Netz und brauchten kein eigenständiges Netz mehr. Deshalb haben wir den Exklusiven Modus ausgeschaltet und beim Setup-Assistenten eine feste IP-Adresse vergeben. Dadurch hatte der Router eine IP-Adresse und leitete die LAN-Pakete sauber weiter. Mit diesen Einstellungen funktionierte der Router tadellos für den Wettbewerb. Leider konnten wir danach nicht mehr über die Router-IP-Adresse auf den Router zugreifen. Wir mussten ihn dann nach dem Wettbewerb auf die Werkseinstellungen zurücksetzen und neu konfigurieren. Wahrscheinlich kann während dem Cup auch gleich das DSLoL-Interface deaktiviert werden.

----
Last edited by Florian Gehrig at 21. August 2015
