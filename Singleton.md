[Back](WikiSolidus)  
[Home](home)  
***
# Singleton
Singleton ist eine Möglichkeit, wie mit Daten umgegangen werden kann, die nur einmal vorkommen sollen.  
Es stellt sicher, dass von einer Klasse genau ein Objekt existiert.
### Programmierung
Der Konstruktor der Klasse sollte **private** gemacht werden.  
Codeteil in der Klasse, die Singleton gemacht werden soll:
>//Die Klasse wird Singleton gemacht  
    private static final Example INSTANCE = new Example();  

Gettermethode:
>//Gettermethode für die Instanz  
public static Example getINSTANCE()  
    {  
        return INSTANCE;  
    }  

"Instanzierung" des Objekts in einer anderen Klasse:
>//Aufruf der Instanz  
private Example ex = Example.getINSTANCE();