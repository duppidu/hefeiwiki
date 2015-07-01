# VirtualBox
----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 22. Juni 2015  
Version: 1.0  
Quellen:  [Thomas Krenn, Netzwerkkonfiguration in VirtualBox](https://www.thomas-krenn.com/de/wiki/Netzwerkkonfiguration_in_VirtualBox) | [CSB, Forum](http://www.csb.vu/threads/fedora-ohne-grafische-oberfl%C3%A4che-wie.121543/) | [Wikipedia, Runlevel](https://de.wikipedia.org/wiki/Runlevel) | [Fedoraproject, Forum](https://ask.fedoraproject.org/en/question/10097/fedora-17-text-mode-screen-resolution/) | [Vincent Verhagen](http://www.vincentverhagen.nl/2008/08/03/how-to-change-console-resolution-on-linux-rhel-centos-fedora-etc/) | [CCM.net](http://ccm.net/faq/40878-fedora-21-switching-to-lxde) | [LXDE Wiki](http://wiki.lxde.org/de/Fedora) | [Raspberry Pi, Forum](https://www.raspberrypi.org/forums/viewtopic.php?f=26&t=14577) | [Chip](http://praxistipps.chip.de/virtualbox-festplatte-nachtraeglich-vergroessern_27503) | [developer-BLOG](https://developer-blog.net/administration/virtualisierung/virtualbox-virtuelle-festplatte-vergroessern/) | [Thomas Krenn, LVM vergrössern](https://www.thomas-krenn.com/de/wiki/LVM_vergr%C3%B6%C3%9Fern) | [Google Developers, Developer Guide](https://developers.google.com/protocol-buffers/docs/overview) | [Google Developers, Java Reference](https://developers.google.com/protocol-buffers/docs/reference/java-generated#package) | [Google Developers, aktueller Compiler](https://developers.google.com/protocol-buffers/docs/downloads) | [Maven Repository, Protocol Buffer Java API](http://mvnrepository.com/artifact/com.google.protobuf/protobuf-java) | [Protobuf Googlecode, Compiler](https://protobuf.googlecode.com/svn/rc/) | [NetBeans Installationsanleitung](https://netbeans.org/community/releases/80/install.html) | [If-not-true-then-false.com](http://www.if-not-true-then-false.com/2014/install-oracle-java-8-on-fedora-centos-rhel/)

----
- <a href="#SM1">Oracle VM VirtualBox</a>
	- <a href="#SM1.1">Netzwerkkonfigurationen</a>
	- <a href="#SM1.2">In Virtualbox nachträglich Festplatten vergrössern</a>
- <a href="#SM2">Fedora</a>
	- <a href="#SM2.1">Text-Modus</a>
	- <a href="#SM2.2">Auflösung im Text-Modus</a>
	- <a href="#SM2.3">LXDE unter Fedora installieren</a>
	- <a href="#SM2.4">NetBeans unter Fedora 21 installieren</a>
- <a href="#SM3">Protobuf</a>
	- <a href="#SM3.1">Java-Compiler unter Linux</a>
	- <a href="#SM3.2">Java-Compiler unter Windows</a> 

----
# <a name="SM1">Oracle VM VirtualBox</a>
## <a name="SM1.1">Netzwerkkonfigurationen</a>
| **Netzwerktyp** | **Zugriff auf andere Gäste** |  **Zugriff von Host**  |  **Zugriff auf externes Netzwerk**  |  
| -------- | -------- |  -------- |  --------  |  
| Not attached | :x: | :x: | :x: |  
| Network Address Translation (NAT) | :x: | :x: | :heavy_check_mark: |  
| Network Address Translation Service | :heavy_check_mark: | :x: | :heavy_check_mark: |  
| Bridged networking | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |  
| Internal networking | :heavy_check_mark: | :x: | :x: |  
| Host-only networking | :heavy_check_mark: | :heavy_check_mark: | :x: |  

**"Not attached" mode**  
In diesem Modus sieht das Gastsystem eine Netzwerkkarte, bei der das virtuelle Netzwerkkabel ausgesteckt ist.

**NAT**  
NAT ist die einfachste Möglichkeit aus dem Gastsystem heraus auf externe Netze zuzugreifen. Ein Zugiff von aussen auf das Gastsystem ist nicht möglich. Auch vom Host-System ist kein Zugriff auf das Gastsystem möglich.

**NAT Service**  
NAT Service ist eine neue NAT-Variante. Die Funktionsweise gleicht einem Router. Ein direkter Zugriff von ausserhalb des Netzwerks auf die Gastsysteme ist nicht möglich. Die Gastsysteme können aber untereinander und nach aussen kommunizieren.

**Bridged networking**  
 In diesem Modus bekommt das Gastsystem direkten Zugriff auf das Netzwerk, an dem auch das Host-System angeschlossen ist.

**Internal networking**  
Bei einem internen Netzwerk können nur Gastsysteme miteinander kommunizieren, die an das gleiche interne Netzwerk angeschlossen sind. Eine Kommunikation zum Host-System oder nach aussen ist nicht möglich.

**Host-only networking**  
In diesem Modus ist eine Kommunikation zwischen angeschlossenen Gastsystemen und dem Host-System möglich. Am Host-System wird dafür ein eigenes virtuelles Netzwerk-Interface verwendet.
## <a name="SM1.2">In Virtualbox nachträglich Festplatten vergrössern</a>
Das Vergrössern der Festplatten in VirtualBox nächträglich, ist möglich aber umständlich. Das System muss ausgeschaltet sein. Über die Kommandozeile von Windows kann die Grösse verändert werden. Zuerst muss auf dem Host-System  der Pfad zur VirtualBox-Installation und der Pfad sowie der Name der virtuellen Festplatte herausgesucht werden.
Beispiel für die Installation: 
***C:\Programme\Oracel\VirtualBox\\***
Beispiel für die virtuelle Festplatte:
***C:\Benutzer\Florian\VirtualBox VMs\Windows10\Windows10.vdi***

In der Windowskonsole wird nun der folgende Befehl eingeben:

	"C:\Programme\Oracle\VirtualBox\VBoxManage.exe" modifyhd "C:[Pfad zum Volume].vdi" --resize 51200

Die Pfade müssen durch die Anfangs gesuchten Pfade ersetzt werden. Mit ***--resize*** wird die Grösse der Festplatte in MB angegeben. Unter dem folgenden Link befindet sich ein praktischer [Umrechner](http://www.umrechnung.org/masseinheiten-datenmenge-umrechnen-bit-byte-mb/datenmenge-filegroesse-speicherplatz.htm).

Nach dem Vergrössern muss die virtuelle Festplatte neu partitioniert werden. Am einfachsten geht es mit Gparted. Dieses Programm ist auch auf der [SystemRescueCD](http://www.sysresccd.org/SystemRescueCd_Homepage) vorhanden. Die SystemRescueCD kann als ISO-Datei heruntergeladen werden und auf dem Gastsystem als virtuelle CD eingebunden werden. Die SystemRescueCD kann im graphischen Modus gestartet werden. Während dem Laden muss noch das Tastaturlayout "de" eingegeben werden. Wird nichts eingegeben wählt das Programm automatisch das Layout "us". Mit Gparted kann dann die Festplatte ausgewählt werden und mit dem Schieber vergrössert werden. Danach muss noch auf den Button zur Ausführung geklickt werden. Sobald die Ausführung abgeschlossen ist. Wird das System neu gestartet.

Um nach dem Partitionieren den zusätzlichen Speicherplatz zu nutzen, bedingt es eine weitere Befehlseingabe auf dem Gastsystem der Virtualbox. Die betreffende virtuelle Festplatte wird mit

	df -h

herausgefunden. Mit dem Befehl 

	resize2fs -p [/dev/mapper/vm208-root]

wird das Dateisystem vergrössert. Der [Pfad] kann je nach verwendetem Gastsystem und Festplattenbezeichnung anders lauten. Mit

	df -h

kann überprüft werden, ob die Vergrösserung funktioniert hat. Die Grösse sollte nun gleich sein, wie bei der Windowskonsole resp. bei Gparted eingestellt wurde.
# <a name="SM2">Fedora</a>
## <a name="SM2.1">Text-Modus</a>
Mit folgenden Code kann das Runlevel eingestellt werde:

	sudo init 3

Die Zahl steht jeweils für das entsprechende Runlevel:  

| **Runlevel** | **Beschreibung** |  
| -------- | -------- |  
| **0** | Shutdown |  
| **S** | Niedriegster Systemzustand für Wartungsarbeitenn, in dem ausschliesslich Systemressourcen wie Festplatten oder Dateisysteme aktiv sind. |  
| **1** | Einzelnutzerbetrieb ohne Netzwerk nur mit lokalen Ressourcen. Oftmals identisch mit "S" |  
| **2** | Lokaler Mehrnutzerbetrieb ohne Netzwerk nur mit lokalen Ressourcen. |  
| **3** | Netzwerkbetrieb, eine grafische Oberfläche ist nicht verfügbar. |  
| **4** | Ist normalerweise nicht definiert. Kann aber für diverse Dienste genutzt werden. |  
| **5** | Wie 3, zusätzlich wird die grafische Oberfläche bereitgestellt. |  
| **6** | Reboot | 

Nach einer Anleitung im Internet kann das System auch dauernd im Text-Modus gestartet werden, wenn die Datei ***/etc/inittab*** als root bearbeitet wird.
Dabei soll die Zeile

	id:5:initdefault:

geändert werden in

	id:3:initdefault:

Der Inhalt der Datei "inittab" zeigt aber:

	# inittab is no longer used.
	#
	# ADDING CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.
	#
	# Ctrl-Alt-Delete is handled by /usr/lib/systemd/system/ctrl-alt-del.target
	#
	# systemd uses 'targets' instead of runlevels. By default, there are two main targets:
	#
	# multi-user.target: analogous to runlevel 3
	# graphical.target: analogous to runlevel 5
	#
	# To view current default target, run:
	# systemctl get-default
	#
	# To set a default target, run:
	# systemctl set-default TARGET.target

Dies bedeutet nun, dass in das Verzeichnis ***/usr/lib/systemd/system*** gewechselt werden muss. Mit dem Befehl,

	systemctl get-default

kann die aktuelle Konfiguration gelesen werden. Mit dem Befehl,

	systemctl set-default TARGET.target

kann die Konfiguration geändert werden. Um nun immer im Text-Modus zu starten muss der Befehl

	systemctl set-default multi-user.target

eingegeben werden. Mit 
	
	systemctl get-default

kann geprüft werden, ob es geklappt hat. Dann sollte stehen,
	
	multi-user.target

## <a name="SM2.2">Auflösung im Text-Modus</a>
Die Shell der Refbox startet nur ab einer bestimmten Auflösung. Die Standardauflösung im Text-Modus von Fedora auf der VirtualBox ist zu klein, sodass die Shell gar nicht startet. Die Auflösung kann über eine Konfigurationsdatei geändert werden. Dazu muss die GRUB-Konfig-Datei geändert werden. Sie ist zu finden unter ***/boot/grub2/grub.cfg***. Dort ist eine Zeile mit *vmlinuz* für den Kernel. Am Ende dieser Zeile muss ***vga=xxx***, z. B. ***vga=792*** eingegeben werden.
Im aktuellen Fall sieht die Zeile folgendermassen aus:

	linux16 /vmlinuz-3.17.4-301.fc21.x86_64 root=/dev/mapper/fedora-root ro rd.lvm.lv=fedora/swap rd.lvm.lv=fedora/root rhgb quiet LANG=de_CH.UTF-8
Nach der Eingabe der gewünschten Auflösung, sollte der Eintrag folgendermassen aussehen:

	linux16 /vmlinuz-3.17.4-301.fc21.x86_64 root=/dev/mapper/fedora-root ro rd.lvm.lv=fedora/swap rd.lvm.lv=fedora/root rhgb quiet LANG=de_CH.UTF-8 vga=773
> Beachte, dass im Bootloader mehere Menüeinträge definiert sein können. Deshalb muss darauf geachtet werden, dass die Änderung im richtigen Menüeintrag, der beim Start standardmässig ausgewählt wird,  vorgenommen wird.

| **Farbtiefe** | **640x480** | **800x600** | **1024x768** | **1280x1024** |   **1400x1050** | **1600x1200** |  
| -------- | -------- | -------- | -------- | -------- | -------- | -------- |  
| **8 (256)** | 769 | 771 | 773 | 775 |  |   |  
| **15 (32K)** | 784 | 787 | 790 | 793 |  |  |  
| **16 (65K)** | 785 | 788 | 791  | 794 | 834 | 884 |  
| **24 (16M)** | 786 | 789 | 792 | 795 |  |  |  

## <a name="SM1.3">LXDE unter Fedora installieren</a>
### LXDE installieren
	yum groupinstall lxde-desktop

### Login Manager konfigurieren

	cd /etc/systemd/system
	rm display-manager.service 
	ln -s /usr/lib/systemd/system/lxdm.service display-manager.service

### LXDE als Standard-Desktop konfigurieren
Die Konfigurationsdatei **/etc/sysconfig/desktop** ändern:
	
	DISPLAYMANAGER=/usr/sbin/lxdm
	PREFERRED=/usr/bin/startlxde

Nachdem diese Befehle ausgeführt wurden, startet Fedora mit der LXDE-Desktopumgebung. Beim Start kann es vorkommen das folgende Meldung erscheint:  

![Openbox_Syntax-Fehler](https://gitlab.com/solidus/hefei/uploads/91227ee2b208aaf898ffa9648bf353c9/Openbox_Syntax-Fehler.png)  

Um den Fehler zu beheben muss die Konfigurationsdatei ***.config/openbox/lxde-rc.xml*** geöffnet werden. Mit grösster Wahrscheinlichkeit wird sie leer sein. Unter dem folgenden Link gibt es eine lange Code-Zeile: [XML-Openbox-Config](XML-Openbox-Config)  

Wird der Code in der Konfigurationsdatei eingefügt und die Datei gespeichert, sollte die Fehlermeldung nicht mehr angezeigt werden.
## <a name="SM2.4">NetBeans unter Fedora 21 installieren</a>
Mit dem Browser über die grafische Oberfläche kann der NetBeans-Installer heruntergeladen werden. Dazu muss vorher noch das aktuelle  Java Development Kit (JDK) von Oracle.com heruntergeladen und installiert werden. Bei der Ausführung der Datei 

	./netbeans-8.0.2-javase-linux.sh 

kommt folgende Fehlermeldung

	Configuring the installer...
	Searching for JVM on the system...
	Extracting installation data...
	Running the installer wizard...
	Can`t initialize UI
	Running in headless mode
	
	Exception: java.awt.HeadlessException thrown from the UncaughtExceptionHandler in thread "main"
Das Problem ist, das OpenJDK installiert wurde. Das die Installation von NetBeans ausgeführt wird, muss auf das Java JDK gewechselt werden. Dies geschieht mit den folgenden Kommandos.
1.Das JDK installieren. Für 32bit-Systeme die erste Zeile für 64bit-Systeme die zweite Zeile eingeben.  

	rpm -Uvh /Pfad/zum/Binary/jdk-8u45-linux-i586.rpm
	rpm -Uvh /Pfad/zum/Binary/jdk-8u45-linux-x64.rpm

2.Installieren von Java, Javaws, libjavaplugin.so und javac

	alternatives --install /usr/bin/java java /usr/java/latest/jre/bin/java 200000
	alternatives --install /usr/bin/javaws javaws /usr/java/latest/jre/bin/javaws 200000
	alternatives --install /usr/lib/mozilla/plugins/libjavaplugin.so libjavaplugin.so /usr/java/latest/jre/lib/i386/libnpjp2.so 200000
	oder
	alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so libjavaplugin.so.x86_64 /usr/java/latest/jre/lib/amd64/libnpjp2.so 200000
	alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
	alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000

3.Aktuelle Version überprüfen

	java -version
	javaws
	javac -version

4.Von OpenJDK auf Java JDK wechseln

	alternatives --config java
	alternatives --config libjavaplugin.so
	oder
	alternatives --config libjavaplugin.so.x86_64
	alternatives --config javac

5.Variable im Profil **/etc/profile file** oder **$HOME/.bash_profile* setzen

	export JAVA_HOME="/usr/java/latest"

Nach der Ausführung dieser Kommandos kann das NetBeans installiert werden.

# <a name="SM3">Protobuf</a>
Protocol Buffers, kurz Protobuf, von Google ist eine eigene Programmiersprache, um auf einfache Weise serialisierte Strukturdaten zu erstellen. Mit der Sprache werden die Schnittstellen beschrieben. Der Code steht dann in einer .proto-Datei bereit. Mit einem Compiler können dann die so erstellten .proto-Dateien für die Implementierung in anderen Sprachen, wie C++, Java und Python, kompiliert werden. Bei Java beispielsweise wird beim Kompilieren eine .java-Datei ausgegeben. Unter den folgenden Links gibt es weiterführende Informationen.

[Google Developers, Developer Guide](https://developers.google.com/protocol-buffers/docs/overview)  

[Google Developers, Java Reference](https://developers.google.com/protocol-buffers/docs/reference/java-generated#package)  

[Google Developers, aktueller Compiler](https://developers.google.com/protocol-buffers/docs/downloads)

[Maven Repository, Protocol Buffer Java API](http://mvnrepository.com/artifact/com.google.protobuf/protobuf-java)  

[Protobuf Googlecode, Compiler](https://protobuf.googlecode.com/svn/rc/)  
>**Achtung!** Die Version der API und des Compilers müssen zwingend übereinstimmen. Andernfalls kann es zu Fehlern kommen.

## <a name="SM3.1">Java-Compiler unter Linux</a>
In das Verzeichnis wechseln

	cd llsf-refbox/src/msgs

Den Source Code von Github herunterladen

	git clone https://github.com/google/protobuf

Nun in den neuen Ordner wechseln

	cd protobuf

Die folgenden Schritte müssen nun ausgeführt werden, um den Compiler zu installieren.
> Ist auch in der Readme-Datei des Compilers beschrieben.

Zuerst die Pakete Automake, Autoconf und Libtool installieren.

	sudo yum install automake autoconf libtool

Mit folgendem Befehl wird "gtest" heruntergeladen und ein Konfigurationsskript geschrieben.

	./autogen.sh

Um nun die C++ Protocol Buffer Runtime und den Protocol Buffer Compiler (protoc) zu installieren, müssen folgende Befehle eingegeben werden:

	./configure
	make
	make check
	sudo make install

Danach kann die Version des Compilers mit

	protoc - -version

überprüft werden.
### Kompilieren
Nach der Installation des Compilers findet sich im Ordner "protobuf" eine neuer Order "java". In diesem Ordner ist wieder eine Readme-Datei zu finden. Die Datei beschreibt drei Arten, um die .proto-Dateien zu kompilieren. Hier wird die dritte Möglichkeit beschrieben.

Zuerst muss in das Verzeichnis mit den .proto-Dateien gewechselt werden. Dort wird ein neuer Ordner erstellt

	mkdir java

Nun wird der Compiler gestartet mit den Angaben von Quell- und Zielort
Syntax:

	protoc -I=\$SRC_DIR --java_out=\$DST_DIR \$SRC_DIR/addressbook.proto

Beispiel:

	protoc -I=./  --java_out=./java (Alle Dateien)
	protoc -I=./  --java_out=./java ./BeaconSignal.proto (Nur die Datei BeaconSingal.proto) 

>**Anmerkung:** Der Compiler hat leider stets einen Syntax-Fehler ausgegeben. Es müsse die Version (Protobuf2 oder Protobuf3) angegeben werden. Leider fanden wir nicht heraus wie das geht. Wir erhielten bei der Nachfrage die bereits kompilierten .java-Files von Alain. Deshalb wurde hier nicht weiter daran gearbeitet.

## <a name="SM3.2">Java-Compiler unter Windows</a>
Unter [Download Protocol Buffers](https://developers.google.com/protocol-buffers/docs/downloads) kann der Compiler für Windows heruntergeladen werden. Die Ordner ins C:\ entzippen. Zudem darin zwei Ordner, "source" und "dest" erstellen und die .proto-Dateien in den Source-Ordner kopieren. Danach die Windowskommandozeile starten. In der Kommandzeile

	cd C:\\[Ordner mit der protoc.exe-Datei]

eingeben, um zum Speicherort des Compilers zu wechseln. Danach die folgende Zeile eingeben
Syntax:

	protoc -I=\$SRC_DIR - -java_out=\$DST_DIR \$SRC_DIR/addressbook.proto

Beispiel:

	protoc -I=source  - -java_out=dest (Alle Dateien)
	protoc -I=source  - -java_out=dest source\BeaconSignal.proto (Nur die Datei BeaconSingal.proto) 

Im Ordner "dest" sollten nun die kompilierten Dateien gespeichert sein. Zum Beispiel,  BeaconSignalProtos.java


----
Last edited by Florian Gehrig at 23. Juni 2015

