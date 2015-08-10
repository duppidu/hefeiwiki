[Home](home) [Back](WikiSolidus)  

***
### Inhalt ###

- <a href="#ak">ExploControllMain</a>
- <a name="ps">prioritySort(String[] string);</a>
- <a name="jh">jobHandler();</a>



***
## <a name="Explo">ExploControllMain</a>
Die Klasse läuft auf einem Lokalen Pc. Von den 3 Robotinos wird jeweils ein String gesendet, welche Felder mit unseren Maschinen belegt sind. Der String wird nur 1 mal betrachtet und verwertet da er überall identisch ist. Ist der String eingetroffen wird er in ein Array von Strings mit je einer Zahl aufgesplittet.  

### <a name="ps">prioritySort(String[] string);</a>
Ist der String aufgesplittet wird das Array der prioritySort Methode übergeben, welche das ex überarbeitet und in eine Liste umlegt. Eine Liste haben wir desshalb gewählt, um die handhabung der abzuarbeitenden Felder zu vereinfachen. Als erstes Suchen wir im Array nach den 2 Sicheren Felder je Team (Cyan 4/9)(Magenta 16/21)
und fügen diese als erstes in die Liste, damit sie als erstes abgearbeitet werden. Danach werden alle anderen Felder hinzugefügt und das Array geleert. Sobald alles Verarbeitet ist, wird mit hilfe der jobHandler Methode die ersten 3 Felder gesendet, welche erkundet werden Sollen.
  
> Wichtig!!!
> Das Program erst kurz vor dem Spielbeginn starten. Sollte ein Robotino bei laufendem Programm auf dem Pc neugestartet werden, gehen die MqttCom's verloren und das Master Package muss neugestartet werden um seine Funktion aufrecht zu erhalten
  
### <a name="jh">jobHandler();</a>
Die Aufgabe der jobHandler Methode ist es, die vorher erstellte Liste der Reihe nach zu versenden. Trifft auf dem Topic /field/explo/getjob eine Robotinonummer (1,2 oder 3) wird im run ein neues Feld gesendet. Dazu wird der sendString Befehl aufgerufen und den jobHandler aufruf als nachricht. Die jobHandler Methode Kopiert dann den obersten Eintrag aus der Liste und löscht diesen da er bearbeitet wird. Ist der Eintrag gelöscht, wird der Kopierte Eintrag als Rückgabewert zurückgegeben.