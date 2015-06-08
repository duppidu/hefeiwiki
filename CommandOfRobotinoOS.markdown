## RobotinoOS

----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 27. Mai 2015  
Version: 1.0  
Quellen:  [Chip](http://praxistipps.chip.de/deutsche-tastatur-in-der-ubuntu-konsole-einrichten_28691) | [askubuntu](http://askubuntu.com/questions/150057/how-can-i-tell-what-version-of-java-i-have-installed) | [nixCraft](http://askubuntu.com/questions/150057/how-can-i-tell-what-version-of-java-i-have-installed)

----
- <a href="#SM1">Aktuelle Konfiguration</a>
- <a href="#SM2">Kommandos</a>

----
### <a name="SM1">Aktuelle Konfiguration</a>
Die Eingabe *uname -a* ergab folgende Ausgabe:
>Linux robotino 3.13.0-32-generic #57-Ubuntu SMP Tue Jul 15 03:51:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

Die Eingabe *getconf LONG_BIT* ergab folgende Ausgabe:
>64

Bei einem Rechtsklick auf die grafische Oberfläche, unter dem Menüpunkt *Version*, geht ein Fenster auf mit folgendem Inhalt:
>Version: 2.0.1

Die Eingabe *java -version* ergab folgende Ausgabe:
>java version "1.8.0_45"
>Java(TM) SE Runtime Environment (build 1.8.0_45-b14)
>Java HotSpot(TM) 64-Bit Server VM (build 25.45-b02, mixed mode)

### <a name="SM2">Kommandos</a>
BIOS-Setup 
>F2 oder Del 

Bootmenue 
>F7

Grafische Oberfläche beenden 
>Ctrl + Alt + Backspace

Java Version überprüfen
>java -version

Installierte Java Versionen
>update-java-alternatives -l

Tastaturlayout ändern
> * sudo dpkg-reconfigure keyboard-configuration
>
> * Generische Tastatur mit 105 Tasten (Intl)
>
> * Deutsch

CPU-Architektur
>**uname -a**  
>Wird *x86_64 GNU/Linux* ausgegeben handelt es sich um einen 64bit Kernel, wenn *i386/i486/i586/i686* steht, handelt es isch um einen 32bit Kernel.
>
>**getconf LONG_BIT**  
>Ausgabe zum Beispiel: **64**
