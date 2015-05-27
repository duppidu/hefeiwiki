**Configuration of RefBox**
----------
**Config-File**
Speicherort: *llsf-refbox/cfg/config.yaml*

**Deafult-Eintrag**

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
    
      clips:
        # Timer interval, in milliseconds
        timer-interval: 40
    
        main: refbox
        debug: true
        # debug levels: 0 ~ none, 1 ~ minimal, 2 ~ more, 3 ~ maximum
        debug-level: 2
        unwatch-facts: [time, rfid-input, signal, gamestate]
        unwatch-rules: [retract-time, rfid-input-cleanup,
                        game-update-gametime-points, game-update-last-time,
                        net-send-beacon, net-send-GameState, net-send-OrderInfo,
                        net-send-MachineInfo, net-send-PuckInfo, net-send-RobotInfo,
                        exploration-send-MachineReportInfo, net-broadcast-MachineInfo,
                        net-send-VersionInfo]
    
      comm:
        protobuf-dirs: ["@BASEDIR@/src/msgs"]
    
        server-port: !tcp-port 4444
        
        public-peer:
          host: !ipv4 137.226.233.255
          port: !udp-port 4444
          #send-port: !udp-port 4444
          #recv-port: !udp-port 4445
    
        cyan-peer:
          host: !ipv4 137.226.233.255
          port: !udp-port 4441
          #send-port: !udp-port 4441
          #recv-port: !udp-port 4446
    
        magenta-peer:
          host: !ipv4 137.226.233.255
          port: !udp-port 4442
          #send-port: !udp-port 4442
          #recv-port: !udp-port 4447
    
      mongodb:
        enable: true
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
        #synchronize refbox time with the time of a simulation 
        time-sync:
          enable: false
          #estimate time by using the last given simulation time speed (helps reducing the amount of messages to send)
          estimate-time: true
**Neue Konfiguration**

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
        test-lights: false
    
      clips:
        # Timer interval, in milliseconds
        timer-interval: 40
    
        main: refbox
        debug: false
        # debug levels: 0 ~ none, 1 ~ minimal, 2 ~ more, 3 ~ maximum
        debug-level: 2
        unwatch-facts: [time, rfid-input, signal, gamestate]
        unwatch-rules: [retract-time, rfid-input-cleanup,
                        game-update-gametime-points, game-update-last-time,
                        net-send-beacon, net-send-GameState, net-send-OrderInfo,
                        net-send-MachineInfo, net-send-PuckInfo, net-send-RobotInfo,
                        exploration-send-MachineReportInfo, net-broadcast-MachineInfo,
                        net-send-VersionInfo]
    
      comm:
        protobuf-dirs: ["@BASEDIR@/src/msgs"]
    
        server-port: !tcp-port 4444
        
        public-peer:
          host: !ipv4 192.168.56.255
          port: !udp-port 4444
          #send-port: !udp-port 4444
          #recv-port: !udp-port 4445
    
        cyan-peer:
          host: !ipv4 192.168.56.255
          port: !udp-port 4441
          #send-port: !udp-port 4441
          #recv-port: !udp-port 4446
    
        magenta-peer:
          host: !ipv4 192.168.56.255
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
        teams: [Solidus]
        crypto-keys:
          Carologistics: randomkey
    
      shell:
        refbox-host: localhost
        refbox-port: 4444
    
      simulation:
        #synchronize refbox time with the time of a simulation 
        time-sync:
          enable: false
          #estimate time by using the last given simulation time speed (helps reducing the amount of messages to send)
          estimate-time: true

  
![100000_HFTM-Logo](https://gitlab.com/solidus/hefei/uploads/618e55dee52192dba6ced79db5811a08/100000_HFTM-Logo.jpg)
