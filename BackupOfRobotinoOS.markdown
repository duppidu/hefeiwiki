## Backup des RobotinoOS

----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 08. Juni 2015  
Version: 1.0  
Quellen:  [SystemRescueCD](http://www.sysresccd.org/SystemRescueCd_Homepage) | [Ubuntu Wiki, Grub, Reperatur](https://wiki.ubuntuusers.de/GRUB_2/Reparatur) | [Ubuntu Wiki, Partimage](https://wiki.ubuntuusers.de/partimage) | [HowtoForge](https://www.howtoforge.com/create-and-restore-partition-images-with-partimage)

----
- <a href="#SM1">Vorbereitungen und Informationen zum Backup</a>
- <a href="#SM2">Backup erstellen </a>
- <a href="#SM3">Backup zurückspielen</a>
- <a href="#SM4">Reperatur</a>

----

## <a name="SM1">Vorbereitungen und Informationen zum Backup</a>
Zwei USB-Sticks bereithalten. Einer ist für die SystemRescueCD, der andere für das Image. Für die CD reichen 4 GB. Die Festplatte des Robotinos ist eine SSD 64GB. Das Image wird aber nur so gross, wie der aktuelle Speicherbedarf ist. Im diesem Fall betrug der Speicherbedarf 4,7GB. Da reichte, ohne Komprimierung, ein 4GB Stick nicht aus. Da auch ohne Komprimierung die Grösse des Images nicht viel Ressourcen auf dem Wiederherstellungsmedium benötigt und die Gefahr von Datenverlust so vermindert werden kann, werden die Sicherungen ohne Komprimierung gemacht. Daher wird ein USB-Stick mit 8GB Speicherplatz benötigt. Ein Stick über 8GB kann aber auch gut verwendet werden, wenn gerade einer vorhanden ist. So kann im Notfall oder zur Sicherheit auch mehr als ein Backup-File gespeichert werden. 

Das Image kann sowohl auf ein FAT32, wie auch auf ein NTFS formatierten Stick geschrieben werden. Um NTFS-Partitionen im Linux einzubinden wird der NTFS-3g-Treiber benötigt. Der sollte aber bei der SystemRescueCD bereits installiert sein. 
Zusätzlich sollte beachtet werden: 
Dass es nur ein File erzeugt, wird bei der Splittung eine Grösse von 6000MB eingestellt. Bei einer 6000MB-Splittung wird das File 4,7GB gross. FAT32 kann nur Dateien verwalten, welche nicht grösser als 4GB sind. 

## <a name="SM2">Backup erstellen</a>  
 1. SystemRescueCD herunterladen.
 2. SystemRescueCD installer herunterladen.
 3. Mit dem Installer die SystemRescueCD auf einen USB-Stick laden.
 4. Stick im Robotino einstecken und starten. Beim Start F7 drücken, um ins Bootmenü zu gelangen. Im Bootmenü den Stick auswählen. Nicht den UEFI-Eintrag auswählen. 
 5. Beim Bootloader von der SystemRescueCD den Eintrag "Direkt in die graphische Oberfläche starten" auswählen. 
 6. Während dem Aufstarten wird nach der "Default-Keymap" gefragt. "de" eingeben für deutsches Tastaturlayout, andernfalls wird das amerikanische Layout geladen.
 7. Den Filemanager (SpaceFM) und PartImage öffnen.
 8. Im Filemanager die zu sichernde Festplatte unmounten (sda1 / 64GB) und das Sicherungsziel mounten.
>Eine Festplatte im NTFS-Format mit zwei Partitionen funktionierte nicht, die Festplatte konnte nur mit einer Partition gemountet werden.

 9. Im Sicherungsziel den Ordner **backup** erstellen.
 10. Im PartImage die Sicherungspartition auswählen. Im Zweiten Schritt das Sicherungsziel: **/media/*Partitionsbezeichnung*/backup/*Sicherungsdateiname*** Beispiel:  **/media/USBDisk/backup/RobiBackup**
 11. Eintrag "Save partition into a new image file" auswählen.
 12. Mit F5 weiter zum nächsten Fenster.
 13. Ohne Komprimierung auswählen. Den Rest kann im Standard belassen werden.
 14. Mit F5 weiter, um die Beschriftung der Sicherung einzugeben.
 15. Das Programm zeigt noch eine kurze Übersicht über den Sicherungsvorgang. Sobald mit Enter bestätigt wurde, beginnt das Programm mit der Sicherung.
 16. Nach dem Abschluss der Sicherung sollte sich auf dem Sicherungsziel mindestens eine Datei befinden: **Sicherungsdateiname.000**

## <a name="SM3">Backup zurückspielen</a>

 1. Die SystemRescueCD aufstarten.
 2. Den Filemanager (SpaceFM) und PartImage öffnen.
 3. Im Filemanager die zu überspielende Festplatte unmounten (sda1 / 64GB) und der Sicherungsort mounten.
 4. Im PartImage die zu überspielende Partition auswählen. Im Zweiten Schritt den Sicherungsort: **/media/*Partitionsbezeichnung*/backup/*Sicherungsdateiname*** Beispiel:  **/media/USBDisk/backup/RobiBackup.000**
 5. Eintrag "Restore partition from an image file" auswählen.
 6. Mit F5 weiter zum nächsten Fenster.
 7. Den Eintrag "Erase free blocks with zero values" auswählen.
 8. Mit F5 weiter zum nächsten Fenster.
 9. Das Programm zeigt noch die Beschreibung an und danach eine kurze Übersicht über den Sicherungsvorgang. Sobald mit Enter bestätigt wurde, beginnt das Programm mit der Wiederherstellung.

Falls das System nach der Wiederherstellung nicht mehr startet und im Grub-Rescue-Modus landet, sollte die Reperatur des Grub weiterhelfen.

## <a name="SM4">Reperatur</a>
Die Reperatur des Grub wurde mit der SystemRescueCD durchgeführt. Da ist man standardmässig als root angemeldet und braucht deshalb kein sudo vor dem jeweiligen Befehl.  

Root-Partition einhängen.
>mount /dev/sda1 /media

Vorbereitung und Wechsel in die chroot-Umgebung.

> - mount -o bind /dev /media/dev  
> - mount -o bind /sys /media/sys  
> - mount -t proc /proc /media/proc  
> - cp /proc/mounts /media/etc/mtab  
>  Überschreiben bestätigen
> - chroot /media /bin/bash

Die GRUB-2-Dateien werden in das Verzeichnis **/boot/grub** installiert und in den MBR des betreffenden Datenträgers geschrieben.
>grub-install /dev/sda

Mit folgendem Befehl wird auf Grundlage der neu installierten Dateien die Datei **/boot/grub/grub.cfg** neu erstellt.
>update-grub

Zum Schluss noch die chroot-Umgebung mit Strg+D verlassen.

----

