## Configuration of the Lancom Router :speak_no_evil:
>Arbeitsschritte die ausgeführt werden müssen, wenn der Lancom-Router auf die Werkseinstellungen zurückgesetzt wurde.  

### Zugriff auf Router
PC-Interface konfigurieren  
IP-Adresse: ***172.23.56.253***  
Netzmaske: ***255.255.255.0***  
Im Browser die Adresse eingeben: ***172.23.56.254***    
Der Router startet mit dem *Default-Setup*.  
### Default-Setup
1. Gerätename: ***LancomRobot***
2. Administrator: ***root***
3. Gerätepassswort: ***soliduscup15***
4. SNMP Read-Only Community: ***private***
5. DHCP-Betriebsart: ***Server***
6. IP-Adresse: ***172.26.0.1***
7. Netzmaske: ***255.255.0.0***

Nach dem Default-Setup im PC-Interface die IP ändern, das LANconfig-Programm öffnen und den Router suchen. Danach im Programm den Setup-Assistent aufrufen.
### Setup-Assistent
1. Setup-Assistent für LancomRobot
2. Internet-Zugang einrichten
3. Eine neue Verbindung anlegen für IPv4
4. Mein Land ist nicht aufgeführt
5. Internet-Zugang über Plain Ethernet (IPoE)
6. Name der Verbindung: INTERNET
7. IP-Parameter automatisch vom DHCP-Server beziehen
8. Keine Verbindungsüberwachung verwenden

### Gerät konfigurieren
![Configuration](https://gitlab.com/solidus/hefei/uploads/e063bf7dfbf355609e66a190435d10ae/Configuration.jpeg)
