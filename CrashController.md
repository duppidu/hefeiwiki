## CrashController  
  
public CrashController()  
  
Im Konstruktor des CrashControllers, werden über JNA der Bumper und in einem Array den die 9 InfrarotSensoren des Roboters instanziert.  
Es werden zudem die Vergleichsdistanzen aus dem drive.xml-File ausgelesen. Der Sensor an der Front benötigt ein grössere Vergleichsdistanz als die Restlichen. Er ist mechanisch weiter hinten montiert.

public synchronized boolean crash()  
  
Die Methode crash() ruft die beiden Methoden infraredSensoring() und bumperControl auf. Sie gibt den wert "true" zurück, sobald eine der beiden aufgerufenen Methoden den Wert "true" zurückgeben.
  
public synchronized boolean infraredSensoring()  
  
Diese Methode ruft ein einer Schlaufe sämtliche Sensorwerte auf und vergleicht diese mit dem parameter. Ist einer der Infrarotwerte kleiner dann gibt die Methode "true" zurück. Der Sensor an der Front (Position 0) wird auf einen anderen Wer verglichen, da er mechanisch weiter hinten montiert ist.
  
public synchronized boolean bumperControl()  
  
Diese Methode gibt den Wert "true" zurück, sobald der Bumper mechanisch unter druck steht.