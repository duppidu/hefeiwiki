[Home](home) [Back](WikiSolidus)

# Inhalt  

- <a name="defConst">LogFact</a>
- <a name="lib">Library</a>
- <a name="neuLog">neuer Logger erstellen</a>
	- <a name="lf">LogFact</a>
	- <a name="lk">zu Loggende Klasse</a>
- <a name="lk">Log Beispiel</a>

### <a name="defConst">LogFact</a>
Leider kann zu die Klasse nicht ins Detail beschrieben werden, da sie bereits zu Beginn
im Konstruktor der Klasse werden alle nötigen Logger erzeugt und die nötigen Einstellungen getroffen. 
Der Logger wird als Instanz so vorbereitet, dass er nur Übergeben werden kann. 


### <a name="lib">Library</a>
In unserem Projekt benutzen wir den Logger Log4J, welcher nicht Standartmässig im Java vorhanden ist. Somit muss auch hier zuerst eine Library im Projekt eingebunden werden um die Feauters nutzen zu können. Die *.jar datei können Sie [hier](https://logging.apache.org/log4j/1.2/download.html) herunterladen. 

### <a name="neuLog">neuer Logger erstellen</a>
Unten werden die Schritte aufgezeigt, welche zum erstellen eines neuen Loggers nötig sind.
 
#### <a name="lf">LogFact</a>
als erstes werden die Variablen bekannt gemacht. Der Name (Master_LOGGER) kann frei gewählt werden, muss dann jedoch im Porjekt durchgehend verwendet werden.  
```
public Logger Master_LOGGER;
```

Danach werden im Konstruktor einige Zeilen hinzugefügt um alle Einstellungen zu treffen wie:  
 - LogLevel
 - Pfad des Logfiles
 - Name des Logfiles

```
//<editor-fold defaultstate="collapsed" desc="Package Master LOGGER">
        this.Master_LOGGER  = org.apache.log4j.Logger.getLogger("Master_LOGGER");
        this.Master_LOGGER.addAppender(consoleAppender);
        this.Master_LOGGER.setLevel(org.apache.log4j.Level.ALL);
        try
        {
            this.Master_LOGGER.addAppender(new FileAppender(detailedLayout, "logs/master.log"));
        }
        catch (IOException ex)
        {
            this.Master_LOGGER.error("Not possible to add fileappender to Master_LOGGER. Message: " + ex.getMessage());
        }
        //</editor-fold>
```
  
Auch die Zeilen einzufügen, um den erstellten Logger zurück zu geben dürfen nicht vergessen werden. 
```
public static Logger getMaster()
    {
        return getInstance().Master_LOGGER;
    }
```

#### <a name="lk">zu Loggende Klasse</a>
auch in der eigenenn Klasse muss zuerst eine Variable bekannt gemacht werden. 
```
private static org.apache.log4j.Logger pc;
```
  
Danach wird der Variabel die vorbereitete Logger instanz übergeben im Konstruktor
```
ProductControllMain.pc = LogFact.getMaster();// Logger
```
Ist alles so weit vorbereitet, hatt der Benutzer folgende Möglichkeiten des Loggers zur verfügung:
Debug Meldungen absetzen
```
pc.debug("Message: Need Job From Robotino 3");
pc.debug("Debug Message", null);
```
Error Meldung absetzen
```
pc.error("Error Message");
pc.error("Error Message", null);
```
Fatal Meldung absetzen
```
pc.fatal("Fatal Message");
pc.fatal("Fatal Message", null);
```



#### <a name="lk">Log Beispiel</a>
Hier ist ein kleiner auszug, zum demonstrieren wie die Logmeldungen aufgebaut sind. 
```
2015-07-22 02:41:58,858 DEBUG [MQTT Call: ExploControllMain] MSG Refbx Zones: -Z13-Z2-Z15-Z16-Z17-Z6-Z19-Z20-Z21-Z22-Z23-Z24 
2015-07-22 02:41:58,858 DEBUG [MQTT Call: ExploControllMain] MSG Refbx Zones: -Z13-Z2-Z15-Z16-Z17-Z6-Z19-Z20-Z21-Z22-Z23-Z24 
2015-07-22 02:41:58,858 DEBUG [MQTT Call: ExploControllMain] MSG Refbx Zones: -Z13-Z2-Z15-Z16-Z17-Z6-Z19-Z20-Z21-Z22-Z23-Z24 
2015-07-22 02:43:13,171 DEBUG [MQTT Call: ExploControllMain] Message: Need ExploJob From Robotino 2 
2015-07-22 02:43:13,327 DEBUG [pool-1-thread-4] Found New Zone to Explore: 15 
2015-07-22 02:43:13,327 DEBUG [pool-1-thread-4] zone removed and returned 
2015-07-22 02:44:09,140 DEBUG [MQTT Call: ExploControllMain] Message: Need ExploJob From Robotino 3 
2015-07-22 02:44:09,281 DEBUG [MQTT Call: ExploControllMain] Message: Need ExploJob From Robotino 1 
2015-07-22 02:44:09,328 DEBUG [pool-1-thread-2] Found New Zone to Explore: 17 
2015-07-22 02:44:09,328 DEBUG [pool-1-thread-2] zone removed and returned 
2015-07-22 02:44:09,625 DEBUG [pool-1-thread-2] Found New Zone to Explore: 6 
2015-07-22 02:44:09,625 DEBUG [pool-1-thread-2] zone removed and returned 
```
