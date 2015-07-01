#  Gripper / Servocontrol

----------
Author: Simon Zeltner 
Class: HF2A 2015
Date: 25.6.2015
Version: 1.0

----------
##  Hardware

To control the gripper we use two standard RC-servos and a Servobrick by thinkerforge.
With this Servobrick you can control up to 7 servos over USB with Java.

![enter image description here](https://www.tinkerforge.com/de/shop/media/catalog/product/cache/2/image/200x200/9df78eab33525d08d6e5fb8d27136e95/b/r/brick_servo_tilted_front_600.jpg)

[Servobrick](https://www.tinkerforge.com/de/shop/servo-brick.html)

[Servo](http://www.servodatabase.com/servo/futaba/s148)

##  Required Software

 - BrickDeamon
 - BrickViewer
 
 Download these programs form the thinkerforge downloadpage.  
 
 [Download](http://www.tinkerforge.com/de/doc/Downloads.html)  


Install the programs with the command sudo dpkg --install "programname"

If there are other packages missing, install them (in my case pm-utils were missing)

sudo apt-get install pm-utils

Try again to install the programs.

There is a good documentation on the thinkerforge webpage which explanes the brickviewer.

##  Java Class ServoControl

The ServoControl Class controls the RC-servos of the gripper.

When the program starts, it defines some parameters for the servobrick. For more details have a look at the Javadoc.

After the the parameters were initialized the program starts to listen to the MQTT Brokertopic "robo/local/grippercontrol".
If this topic receives a message called "open", the ServoControl program triggers the Servobrick and gives the servos the command to go to their "open"-position.
If the topic receives a message called "close" instead, the ServoControl program triggers the Servobrick and gives the servos the command to go to their "close"-position.

Every open/close process will be displayed as a system output.


###  Diagram

![Servo](https://gitlab.com/solidus/hefei/uploads/c8b25efd7d5be614823c1d5a4135b167/Servo.JPG)
