Raspberry Pi als Local Git Server
===================
Wir Verwenden während des Robocps zusätzlich zu den Robotinos zusätzlich 2 Raspberry pi
Die Raspberry Übernehmen folgende Aufgaben:
> - Zentraler MQTT Broker für die Kommunikation der Robotinos
> - Lokales GitLab Während des Cups (zur unabhängigkeit vom Internet)



## Installation
#### Vor der Installation Bringen wir die Software auf dem Raspberry auf den neusten Stand
```
sudo apt-get update
sudo apt-get upgrade
```
Nachdem der der Upgrade-Befehl ausgeführt wurde Wird nachgefragt ob der Benötigte Speicher belegt werden Soll -> Möchten Sie Fortfahren [ J/N ] 
Mit J und Enter bestätigen  


#### Nun Installieren wir Git auf dem Raspberry:
```
sudo apt-get install git
```
Ist Git bereits Installiert wir dies angezeigt.  
Ist das Programm nicht installiert, wird wider nachgefragt ob der Benötigte Speicher belegt werden Soll 
-> Möchten Sie Fortfahren [ J/N ]


## Konfigurieren und Initialisieren