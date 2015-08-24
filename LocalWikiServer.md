[Home](home) [Back](WikiSolidus)


Raspberry Pi als Local Git Wiki Server
===================


- <a href="#in">Installation</a>
- <a href="#ki">Konfiguration Raspberry</a>
- <a href="#kn">Konfiguration Netbeans</a>
- <a href="#da">Direktes Aktualisieren</a>


Wir Verwenden während des Robocps zusätzlich zu den Robotinos 2 Raspberry pi
Die Raspberry Übernehmen folgende Aufgaben:
> - Zentraler MQTT Broker für die Kommunikation der Robotinos
> - Lokales GitLab Während des Cups (zur unabhängigkeit vom Internet)


Den Test während des Cups hatt das System jedoch nicht bestanden. Auf dem Raspberry ist der Gollum Server einfach zu langsam. Es ist Jedoch praktisch, wenn wie wir in China kein richtiger Zugang zum Internet vorhanden ist und informationen aus dem Wiki geholt werden müssen. 
Ein Weiterer Nachteil ist, dass jegliche änderungen welche so gemacht werden als Anonym angezeigt werden und nicht mit dem Benutzernamen.



## <a name="in">Installation
#### Vor der Installation Bringen wir die Software auf dem Raspberry auf den neusten Stand
```
sudo apt-get update
sudo apt-get upgrade
```
Nachdem der Upgrade-Befehl ausgeführt wurde Wird nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ] 
Mit J und Enter bestätigen  


#### Nun Installieren wir Gollum auf dem Raspberry:
```
gem install gollum
```
Ist gollum bereits Installiert wir dies angezeigt:
git ist schon die neueste Version  

Ist das Programm nicht installiert: 
wird wider nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ]


## <a name="ki">Konfigurieren und Initialisieren (PI)

Nun ist die Software soweit fertig und wir begeben uns zur Konfiguration
mit:
```
cd ~
```
Wechseln wir ins Home verzeichniss des Users. 
Nun wir die Ordnerstruktur für das Git Projekt
```
mkdir Solidus
```
ist der Ordner Solidus bereits vorhanden, muss er nicht erneut erstellt werden.  
Mit
```
cd Solidus
```
```
git clone git@gitlab.com:solidus/hefei.wiki.git
```
Wird das Wiki von Online auf das Raspberry kopiert. 
Wir wechseln in den Ordner mit dem Projekt
```
cd hefei.wiki
```
Sind wir im Ordner angelangt starten wir mit dem Befehl
```
gollum
```
Den Server, welcher eine Internetseite mit dem Wiki Onlineschaltet. 