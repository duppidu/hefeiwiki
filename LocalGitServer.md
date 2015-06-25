[Home](home) [Back](WikiSolidus)


Raspberry Pi als Local Git Server
===================
Wir Verwenden während des Robocps zusätzlich zu den Robotinos 2 Raspberry pi
Die Raspberry Übernehmen folgende Aufgaben:
> - Zentraler MQTT Broker für die Kommunikation der Robotinos
> - Lokales GitLab Während des Cups (zur unabhängigkeit vom Internet)



## Installation
#### Vor der Installation Bringen wir die Software auf dem Raspberry auf den neusten Stand
```
sudo apt-get update
sudo apt-get upgrade
```
Nachdem der Upgrade-Befehl ausgeführt wurde Wird nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ] 
Mit J und Enter bestätigen  


#### Nun Installieren wir Git auf dem Raspberry:
```
sudo apt-get install git
```
Ist Git bereits Installiert wir dies angezeigt:
git ist schon die neueste Version  

Ist das Programm nicht installiert: 
wird wider nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ]


## Konfigurieren und Initialisieren (PI)

Nun ist die Software soweit fertig und wir begeben uns zur Konfiguration
mit:
```
cd ~
```
Wechseln wir ins Home verzeichniss des Users. 
Nun wir die Ordnerstruktur für das Git Projekt
```
mkdir Solidus
cd Solidus
mkdir hefei.git
cd hefei.git
```
Nun ist es an der Zeit ein neues und Leeres Git Repository zu initialisieren
```
git init --bare
```
Damit ist auf dem Raspberry alles Vorbereitet

## Konfigurieren (Netbeans)
 Laden des aktuellen codes auf das Pi. Darum als erstes die Aktuellen Codezeilen Herunterladen
- > Git  
- >> Remote 
- >>> Pull 

Push Menue aufrufen (rechtsklick auf Projekt)
> - Git  
> - - Remote  
> - -- Push  

im Push Fenster Wählen wir:
```
Specify Git Repository Location 
```
Remote Name:
```
origin /Persitst Remote yes
```
Repository URL:
```
172.26.0.3:/home/pi/Solidus/hefei.git
```
Username:
```
pi
```
 

## Direktes Aktualisieren des PI
Nun geben wir Git die Addresse des Projekts auf Gitlab um direkt zu Synchronisieren

damit haben wir die Addresse unter dem namen origin gespeichert
Nun folg der Abgleich mit dem WWW
```
git fetch origin +refs/heads/*:refs/heads/* --prune
```
kein git pull möglich

mit 
```
git log main
```
(main steht für den Branch) Sollte nun der letzte Aktuelle Commit zu Sehen seit



Um das Repository im WWW zu aktualisieren wird 
```
git push
```
verwendet. Nach der Angabe von Online Benutzername und Passwort sollte das
Online Repo wider auf dem neusten Stand Sein
