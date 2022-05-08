# nvidia-project
# The idea of this project is to develop a program that can be of help for the blind. 
# By taking the command from the user to start the recognition, it can be very helpful for the blind simplifying some tasks
# By detecting objects, it is very important for blind people who require the help of someone to guide them while walking around.
# This program works by detecting the image with detectnet for object detection.
# It then gives the detection by speech by text to speech conversion via gtts.

# Make sure you are using your Jetson Nano with an hdmi device containing speakers
# You will need to be a root user first by running:
sudo su
# You will need to go into a file called "default.pa" located in "/etc/pulse"
nano /etc/pulse/default.pa
# Go to the second to last line in the file where you will find "#set-default-sink output", change it to:
set-default-sink 0
# Now your device is capable of producing audio on your hdmi device

# For the audio also, you will need to install two libraries "gTTS" and "playsound" by running:
pip3 install gTTS playsound.


# You should already have the jetson-inference directory setup but if you haven't make sure to do the following steps:

sudo apt-get update
sudo apt-get install git cmake
git clone https://github.com/dusty-nv/jetson-inference
cd jetson-inference
git submodule update --init
sudo apt-get install libpython3-dev python3-numpy
mkdir build
cd build
cmake ../
# It is enough to download resnet, googlenet and most importantly SSD-Mobilenet-v2 (the one it uses)
# You can then skip the pytorch download
# After finishing the downloads, run:
make
sudo make install
sudo ldconfig


# Now you can run the project by running the command below (make sure you only have one camera plugged into your device):
python3 project.py /dev/video0
# Make sure you are connected to the internet while running the code.
# If you want to see what the camera is showing, make sure you run the code in headed mode.

# Video demonstration below
https://youtu.be/aNS7IQPl4QQ
