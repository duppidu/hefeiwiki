
# Programming with ALVAR


----------
Author: Simon Zeltner 
Class: HF2A 2015
Date: 9.6.2015
Version: 1.0
specific for the Robotinoproject

----------

Because the CMAKE program is to complicated to use with an own cmakelists file we decided to use a sample program and change it for our needs. This means for installing the changes you made within the sample program you can use the normal cmake files which come already with the ALVAR library.

## Make changes and compile the program properly

First make sure you've installed the ALVAR library correctly (have a look at the ALVAR install manual).

After you installed the library properly you should have a folder which is called "sample".

alvar-2.0.0-sdk-linux64-gcc44/build/build_gcc44_release/sample

In this folder you find all the sampleprograms you can use to make changes. So i used the SampleMarkerDetector.cpp (for the ID-Detection) and SampleMarkerHide.cpp (for the coordinates).

After you made your changes you have to save the file **with the same name like before!**. Then you have to change the directory to 
alvar-2.0.0-sdk-linux64-gcc44/build/build_gcc44_release 

After this you have to run the command "sudo make install" to compile and install your changes. 

This should run properly if OpenCv ist installed. As soon as everything's finished you can start your program in the folder

alvar-2.0.0-sdk-linux64-gcc44/bin

For starting you have to use "sudo ./"programname".



> Written with [StackEdit](https://stackedit.io/).
