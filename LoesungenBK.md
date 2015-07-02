[Home](home)  
[DokuSolidus](DokuSolidus)  

---------------------

# WaAnalyzer



# Drive

Durch Absprache mit dem Team wurde bei der goToTarget Methode die machineAlign Methode hinzugefügt damit diese automatisch durch das Drive aufgerufen wird. Die machineAlign und targetAlign Methode wurden zur Align Methode zusammengeführt. Der Grund dafür ist dass diese Methoden sehr ähnlich sind und durch wenige Änderungen zusammengeführt werden können. Die Kommunikation zwischen WayAnalyzer und Drive wurde mittels Speed Klasse realisiert. Diese wird vom WayAnalyzer geschrieben und dann über den Broker gesendet. Das Drive empfängt diese Klasse dann und überschreibt danach die eigenen Geschwindigkeiten.