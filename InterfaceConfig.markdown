# Interface Config

----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 05. Juni 2015  
Version: 1.0  
Quellen:  [Ubuntu Wiki, Interfaces](https://wiki.ubuntuusers.de/interfaces) | [bits meets Bytes, Verschlüsselungen](http://bits-meet-bytes.de/wlan-verschluesselungsmethoden/) | [PCWELT, Verschlüsselungen](http://www.pcwelt.de/tipps/Die_richtige_WLAN-Verschluesselung_fuer_Ihren_Router-WLAN-Einstellungen-7567027.html) 

----
- <a name="SM1">interface</a>  
- <a name="SM2">wpa_supplicant.conf</a>  
- <a name="SM3">Weitere Erläuterungen zu den Konfigurationen</a>  

----
## <a href="#SM1">interface</a>
>/etc/network/interface

	# This file describes the network interfaces available on your system
	# and how to activate them. For more information, see interfaces(5).
	
	# The loopback network interface
	auto lo
	iface lo inet loopback
	
	# The primary network interface (fallback)
	auto em1
	iface em1 inet dhcp

	auto wlan0
	iface wlan0 inet manual
	wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
	wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
	
	iface default inet static
	address 172.26.1.3
	netmask 255.255.0.0
	network 172.26.0.0
	broadcast 172.26.255.255
	gateway 172.26.0.1
	dns-nameservers 172.26.0.1
## <a href="#SM2">wpa_supplicant.conf</a>
>etc/wpa_supplicant/wpa_supplicant.conf

	ctrl_interface=/var/run/wpa_supplicant
	eapol_version=1
	ap_scan=1

	network={
	   ssid="RobotinoEvent.1"
	   scan_ssid=1
	   psk="soliduscup15"
	   proto=RSN
	   key_mgmt=WPA-PSK
	   group=CCMP
	   pairwise=CCMP
	}
## <a href="#SM3">Weitere Erläuterungen zu den Konfigurationen</a>
**PSK**  
Pre-Shared Key = Schlüssel

**Verschlüsselung**  

| Verschlüsselungsstandard | Sicherheitsprotokoll | Verschlüsselungsalgorithmus |  
| -------- | -------- | -------- |  
| WEP (Wired Equivalent Privacy) | - | - |  
| WPA (Wi-Fi Protected Access) | TKIP (Temporal Key Integrity Protocol) | - |  
| WPA2 (Wi-Fi Protected Access 2) | CCMP (Counter Mode with <br> Cipher Block Chaining Message Authentication Code Protocol) | AES (Advanced Encryption Standard) |   

WPA2 wird manchmal auch als WPA2-Personal oder WPA2-Enterprise bezeichnet. Personal ist die normale Verschlüsselung, welche häufigsten privat eingesetzt wird. Enterprise ist eine WPA2-Verschlüsselung mit einem RADIUS-Server.

**RADIUS-Server**  
Der RADIUS-Server ist Bestandteil von WPA2-Enterprise. Wenn die Enterprise-Verschlüsselung aktiviert ist, muss ein WLAN-Benutzer sich beim Verbinden, am RADIUS-Server mit seinen Login-Daten einloggen. Die HFTM benutzt für ihr Studenten-WLAN-Zugang auch einen RADIUS-Server.

**auto** [Interface]  
Bedeutet dass das Interface beim Booten automatisch gestartet wird.

**iface**  
Ist die Abkürzung für Interface.

**Interface (eth0, wlan0, ...)**  
Da kann explizit das Interface angegeben werden.

**inet**  
Ist das Protokoll und bedeutet, die Verbindung geht ins Internet.

**static**  
Das ist die Methode. Mit *static* wird eine statische Konfiguration erwartet, bei *dhcp* muss nichts weiter konfiguriert werden, das Interface holt sich die benötigten Informationen über den DHCP-Server. Wird *manual* eingegeben, bleibt das Interface unkonfiguriert.

------
**Remapping**  
Für das Remapping wird die Methode *manual* benötigt. Das betreffende Interface bekommt die Methode *manual*. Dann wird ein weiteres Interface mit einem Fantasienamen konfiguriert, z. B. *work* oder *home*. Bei diesem Interface wird dann die richtige Konfiguration vorgenommen. Das könnte dann folgendermasse aussehen:

	iface eth0 inet manual
	iface default inet dhcp
	iface work inet static
		address 192.168.0.10
		netmask 255.255.255.0
		gateway 192.168.0.1
Beim Systemstart wird nun das Interface unkonfiguriert geladen. Mit dem Befehl

	sudo ifup eth0=work
kann dann die statische Konfiguration geladen werden. Oder mit

	sudo ifup eth0=default
die dynamische Kofiguration.

**Einstellungen aktivieren**  
Um die neuen Einstellungen zu übernehmen, können alle Interfaces mit einem *auto* Eintrag neu gestartet werden. Mit dem Befehl:

	sudo /etc/init.d/networking restart
Für die Schnittstellen ohne *auto* Eintrag gilt folgender Befehl:

	sudo ifup [Schnittstelle]
Falls die Einstellungen nicht übernommen werden, muss das System neu gestartet werden.

