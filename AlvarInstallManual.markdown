
# ALVAR 2.0.0 SDK Installation Manual LINUX


----------
Author: Simon Zeltner  
Class: HF2A 2015  
Date: 25.5.2015  
Version: 1.0

----------


 1. Download package alvar-2.0.0-sdk-linux64-gcc44.tar.gz from the Alvar Website (you have to fill out the form!)
 2. Extract the package
 3. Download and install OpenCV Dev -> sudo apt-get install libopencv-dev
 4. Download and install GLUT -> sudo apt-get install freeglut3-dev
 5. Download and install OpenSceneGraph -> sudo apt-get install openscenegraph
 6. Download and install Cmake -> sudo apt-get install cmake
 7. Download and install g++4.4 with sudo apt-get install g++-4.4
 8. Got to your Alvar folder, open the build folder and make the generate*.sh files runnable with sudo chmod +x generate*.sh and run generate_gcc44.sh with ./build/generate_gcc44.sh
 9. Enter the new created folder /build/build_gcc44_release/build
 10. run  sudo cmake .
 11. If CMake cannot find the required libraries configure the following variables according to your development
   environment.
     OpenCV_ROOT_DIR = /path/to/opencv
     GLUT_ROOT_PATH = /usr
     OSG_ROOT_DIR = /usr
     
 12.  build and install the project with the command sudo make install 
 
 # # Errorhelp
1. Copy the Alvarplugins folder from bin to the samples folder if you have the Error "cannot find any capture plugins" while running a sampleprogram.
2. If you get OpenGl Errors, run this command export LIBGL_ALWAYS_SOFTWARE=1
