# Refbox Konfiguration

----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 08. Juni 2015  
Version: 2.0  

----
- <a href="#SM1">Config-File</a>
- <a href="#SM2">Default-Eintrag</a>
- <a href="#SM3">Neue Konfiguration</a>

----
## <a name="SM1">Config-File</a>
>Speicherort: *llsf-refbox/cfg/config.yaml*

## <a name="SM2">Default-Eintrag</a>

	   %YAML 1.2
	%TAG ! tag:fawkesrobotics.org,cfg/
	---
	# Configuration meta information document
	include:
	  # reads files ending in .yaml from conf.d config subdir
	  # - !ignore-missing conf.d/
	  # Reads the host-specific configuration file, no failure if missing
	  - !host-specific host.yaml
	---
	# Main configuration document
	
	llsfrb:
	  log:
	    level: info
	    general: refbox.log
	    clips: clips.log
	    game: game.log
	
	  sps:
	    enable: false
	    host: !ipv4 192.168.1.77
	    port: !tcp-port 502
	    test-lights: true
	
	  mps:
	    enable: true
	    # type: 1(incoming station), 2(singel p&p), 3(double p&p), 4(delivery station)
	    stations:
	      C-BS:
	        active: false
	        type: BS
	        host: !ipv4 192.168.2.27
	        port: !tcp-port 502
	      C-CS1:
	        active: false
	        host: !ipv4 192.168.2.24
	        port: !tcp-port 502
	        type: CS
	      C-CS2:
	        active: false
	        host: !ipv4 192.168.2.25
	        port: !tcp-port 502
	        type: CS
	      C-RS1:
	        active: false
	        host: !ipv4 192.168.2.23
	        port: !tcp-port 502
	        type: RS
	      C-RS2:
	        active: true
	        host: !ipv4 192.168.2.26
	        port: !tcp-port 502
	        type: RS
	      C-DS:
	        active: false
	        host: !ipv4 192.168.2.28
	        port: !tcp-port 502
	        type: DS
	      M-BS:
	        active: false
	        host: !ipv4 192.168.2.33
	        port: !tcp-port 502
	        type: BS
	      M-CS1:
	        active: false
	        host: !ipv4 192.168.2.30
	        port: !tcp-port 502
	        type: CS
	      M-CS2:
	        active: false
	        host: !ipv4 192.168.2.32
	        port: !tcp-port 502
	        type: CS  
	      M-RS1:
	        active: false
	        host: !ipv4 192.168.2.31
	        port: !tcp-port 502
	        type: RS
	      M-RS2:
	        active: false
	        host: !ipv4 192.168.2.34
	        port: !tcp-port 502
	        type: RS
	      M-DS:
	        active: false
	        host: !ipv4 192.168.2.29
	        port: !tcp-port 502
	        type: DS
	
	  clips:
	    # Timer interval, in milliseconds
	    timer-interval: 40
	
	    main: refbox
	    debug: true
	    # debug levels: 0 ~ none, 1 ~ minimal, 2 ~ more, 3 ~ maximum
	    debug-level: 2
	    unwatch-facts: [time, signal, gamestate]
	    unwatch-rules: [retract-time,
	                    game-update-gametime-points, game-update-last-time,
	                    net-send-beacon, net-send-GameState, net-send-OrderInfo,
	                    net-send-MachineInfo, net-send-RobotInfo,
	                    exploration-send-MachineReportInfo, net-broadcast-MachineInfo,
	                    net-send-VersionInfo]
	
	  comm:
	    protobuf-dirs: ["@BASEDIR@/src/msgs"]
	
	    server-port: !tcp-port 4444
	    
	    public-peer:
	      #host: !ipv4 192.168.122.255
	      host: !ipv4 127.0.0.1
	      #port: !udp-port 4444
	      send-port: !udp-port 4444
	      recv-port: !udp-port 4445
	
	    cyan-peer:
	      #host: !ipv4 192.168.122.255
	      host: !ipv4 127.0.0.1
	      #port: !udp-port 4441
	      send-port: !udp-port 4441
	      recv-port: !udp-port 4446
	
	    magenta-peer:
	      #host: !ipv4 192.168.122.255
	      host: !ipv4 127.0.0.1
	      #port: !udp-port 4442
	      send-port: !udp-port 4442
	      recv-port: !udp-port 4447
	
	  mongodb:
	    enable: false
	    hostport: localhost
	    collections:
	      text-log: llsfrb.log
	      clips-log: llsfrb.clipslog
	      protobuf: llsfrb.protobuf
	
	  game:
	    teams: [Carologistics]
	    crypto-keys:
	      Carologistics: randomkey
	
	  shell:
	    refbox-host: localhost
	    refbox-port: 4444
	
	  simulation:
	    enable: false
	    # synchronize refbox time with the time of a simulation 
	    time-sync:
	      enable: false
	      # estimate time by using the last given simulation time speed
	      # (helps reducing the amount of messages to send)
	      estimate-time: true
 
----------
## <a name="SM3">Neue Konfiguration</a>

	   	%YAML 1.2
	%TAG ! tag:fawkesrobotics.org,cfg/
	---
	# Configuration meta information document
	include:
	  # reads files ending in .yaml from conf.d config subdir
	  # - !ignore-missing conf.d/
	  # Reads the host-specific configuration file, no failure if missing
	  - !host-specific host.yaml
	---
	# Main configuration document
	
	llsfrb:
	  log:
	    level: debug # Wird zum Entwickeln auf Debug gestellt.
	    general: refbox.log
	    clips: clips.log
	    game: game.log
	
	  sps:
	    enable: false
	    host: !ipv4 192.168.1.77
	    port: !tcp-port 502
	    test-lights: true
	
	  mps:
	    enable: false # Die MPS muss auf false sein, da keine zur Verfügung steht.
	    # type: 1(incoming station), 2(singel p&p), 3(double p&p), 4(delivery station)
	    stations:
	      C-BS:
	        active: false
	        type: BS
	        host: !ipv4 192.168.2.27
	        port: !tcp-port 502
	      C-CS1:
	        active: false
	        host: !ipv4 192.168.2.24
	        port: !tcp-port 502
	        type: CS
	      C-CS2:
	        active: false
	        host: !ipv4 192.168.2.25
	        port: !tcp-port 502
	        type: CS
	      C-RS1:
	        active: false
	        host: !ipv4 192.168.2.23
	        port: !tcp-port 502
	        type: RS
	      C-RS2:
	        active: true
	        host: !ipv4 192.168.2.26
	        port: !tcp-port 502
	        type: RS
	      C-DS:
	        active: false
	        host: !ipv4 192.168.2.28
	        port: !tcp-port 502
	        type: DS
	      M-BS:
	        active: false
	        host: !ipv4 192.168.2.33
	        port: !tcp-port 502
	        type: BS
	      M-CS1:
	        active: false
	        host: !ipv4 192.168.2.30
	        port: !tcp-port 502
	        type: CS
	      M-CS2:
	        active: false
	        host: !ipv4 192.168.2.32
	        port: !tcp-port 502
	        type: CS  
	      M-RS1:
	        active: false
	        host: !ipv4 192.168.2.31
	        port: !tcp-port 502
	        type: RS
	      M-RS2:
	        active: false
	        host: !ipv4 192.168.2.34
	        port: !tcp-port 502
	        type: RS
	      M-DS:
	        active: false
	        host: !ipv4 192.168.2.29
	        port: !tcp-port 502
	        type: DS
	
	  clips:
	    # Timer interval, in milliseconds
	    timer-interval: 40
	
	    main: refbox
	    debug: true # Ist das Debuggen eingeschaltet, werden Meldungen in der Shell ausgegeben.
	    # debug levels: 0 ~ none, 1 ~ minimal, 2 ~ more, 3 ~ maximum
	    debug-level: 3 # Mit dem Debuglevel 3 werden alle Meldungen ausgegeben, auch das BeaconSignal.
	    unwatch-facts: [time, signal, gamestate]
	    unwatch-rules: [retract-time,
	                    game-update-gametime-points, game-update-last-time,
	                    net-send-beacon, net-send-GameState, net-send-OrderInfo,
	                    net-send-MachineInfo, net-send-RobotInfo,
	                    exploration-send-MachineReportInfo, net-broadcast-MachineInfo,
	                    net-send-VersionInfo]
	
	  comm:
	    protobuf-dirs: ["@BASEDIR@/src/msgs"]
	
	    server-port: !tcp-port 4444
	    
	    public-peer:
	      host: !ipv4 192.168.56.255 # Die Broadcast-Adresse kommt vom Host-only-Adapter von der Virtualbox.
	      #host: !ipv4 127.0.0.1
	      port: !udp-port 4444 # Je nach Anwendung muss der Port für das Senden und Empfangen gleich sein.
	      #send-port: !udp-port 4444
	      #recv-port: !udp-port 4445
	
	    cyan-peer:
	      host: !ipv4 192.168.56.255
	      #host: !ipv4 127.0.0.1
	      port: !udp-port 4441
	      #send-port: !udp-port 4441
	      #recv-port: !udp-port 4446
	
	    magenta-peer:
	      host: !ipv4 192.168.56.255
	      #host: !ipv4 127.0.0.1
	      port: !udp-port 4442
	      #send-port: !udp-port 4442
	      #recv-port: !udp-port 4447
	
	  mongodb:
	    enable: false
	    hostport: localhost
	    collections:
	      text-log: llsfrb.log
	      clips-log: llsfrb.clipslog
	      protobuf: llsfrb.protobuf
	
	  game:
	    teams: [Solidus] # Der Teamname muss eingetragen werden.
	    crypto-keys:
	      Solidus: randomkey # Für den privaten Kanal muss ein Schlüssel eingegeben werden.
	
	  shell:
	    refbox-host: localhost
	    refbox-port: 4444
	
	  simulation:
	    enable: true # Falls die MPS auf false ist, muss dafür die Simulation auf true sein.
	    # synchronize refbox time with the time of a simulation 
	    time-sync:
	      enable: false
	      # estimate time by using the last given simulation time speed
	      # (helps reducing the amount of messages to send)
	      estimate-time: true

	      
----
Last edited by Florian Gehrig at 10. Juli 2015
