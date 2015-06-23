#  Markerdetection

Author: Simon Zeltner  
Class: HF2A 2015  
Date: 25.5.2015  
Version: 1.0  

### Miscellaneous

The Markerdetection class is a standalone class. This means it just has to be instanced in it's own main method and runs completely for itself. 

###  Explanation

The markerdetection for the Robotino runs with ALVAR ( for more information visit the seperate documentation). Because ALVAR only runs with C++, we made a workaround. We use JNA (Java Native Access) to start a C++ program which does the markerdetection.

### Explanation C++ Program

We used a sampleprogram from the ALVAR Library and made some adaptions to it. We did it like that because the cmake files were to complicated to change in our amount of time (for more information have a look at "Programming with alvar"). The file we changed is called  "sampleMarkerDetection.cpp".

The function of the C++ program is pretty simple. First it starts the camera and grabs the videostream of it. Then it searches ALVAR markers (could also search for AR_Toolkit Markers) in this videostream. If a marker is detected, his ID will be written into a file which is created also by the program. If nothing is detected, the file will be deleted (first safety).

###  Explanation Java Program

The Java program is here to do the JNA stuff. It's pretty simple to understand too.

As soon the a new instance of the code will be made, the program starts running. At first it starts the C++ program. Then the Java program looks for the file the C++ program created. If the file exists, the Java part reads out the first line in the file. If it's empty nothing will be sent (second safety). As soon the first line contains something, the java part notices that a marker has been detected. It reads the ID in the file and saves it to a local String and also deletes the file (third safety). This string will now be sent to the MQTT Broker. After the message has been sent, the Java part stops the C++ program and after this it shuts down himself.

### Explanation Safetys

Problem:

We detected the problem when the marker is still in the picture when the program shuts down. It generated a new file which shouldn't happen. In this case, when the program restarts, the file is already there **but with the old ID!**.

Solution:

The key of this program is to get the right marker ID in the right moment. So to bypass this problem we programmed a 3 Level Safetysystem. The safetys make sure the file has been deleted so the program can't get a wrong ID due to a late safed MarkerID.

Safety 1: If the file exists, but nothing is in it, it will be deleted.
Safety 2: The C++ program deletes the file.
Safety3: The Java program deletes the file.

#  Markercoordinates

We need the Coordinates of the ALVAR marker to align the Robotino to the MPS. For this a C++ program takes the X-coordinates the marker has in the videopicture (0 is right).

The way it works is pretty much the same as the way of the markerdetection. The only difference is that there is no MQTT communication. There is a method in the Java program, which returns the X-coordinates value.




> Written with [StackEdit](https://stackedit.io/).