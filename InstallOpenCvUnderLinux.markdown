# Install OpenCv under Linux with Java Support

We need OpenCv for the Lamp Detection and the ALVAR-Tag detection. Because the Robotino runs a Linux System (Ubuntu) we cannot use the installation manuals for Windows which are mostly more detailed than Linux Versions.

## Installation

1) So first you have to download your OpenCv Version and **make sure a Java JDK ist installed!**
-> http://opencv.org/downloads.html

2) **Make sure your JAVA_HOME path is also set as root!**
		

	sudo su JAVA_HOME=/usr/lib/jvm/java-8-oracle 
	-> This is the path in my case, yours could be different


3) Unpack the package and enter your received folder.

4) Generate a new folder called "release" with the command

		sudo mkdir release
5) Run the cmake command

		cmake -DBUILD_SHARED_LIBS=OFF ..
6) After the command is finished without errors check if the java parts are properly compiled

![Screenshot_-_16.06.2015_-_08_58_16](https://gitlab.com/solidus/hefei/uploads/0211be0f91a8adda38a101ed34bb9811/Screenshot_-_16.06.2015_-_08_58_16.png)

7) Install the Library with 

		sudo make install
Please stay calm, this could take a while (30min)

8) After the installation is finished, you have to copy 2 files so the system can recognize them.
Copy the opencv-"version".jar file ( you can find it in your release/bin) to /usr/lib
and the opencv-"version".so file (you can find it in your release/lib) also to /usr/lib

For example:
		
		~/opencv-2.4.11/release/bin$ sudo cp opencv-2411.jar /usr/lib
		
After this your OpenCv Library should be successful installed.


