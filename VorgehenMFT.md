## ColorDetection

Das Device Problem das durch die momentan verbuggte OpenCV Version und dem Problem des C++ Teiles der Markerdetection verursacht wurde konnte durch den separaten Aufruf der ColorDetection behoben werden.   
Die ColorDetection wird nun in einem separaten .jar aufgerufen somit hat dieser Programmteil einen eigennen Prozess auf dem Robotino und durch dies lässt sich diese auch ohne Problem wider schliessen.