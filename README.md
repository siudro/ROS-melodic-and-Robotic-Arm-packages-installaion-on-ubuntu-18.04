# ROS-melodic-and-Robotic-Arm-packages-installaion-on-ubuntu-18.04
## installing robot operating system (ROS) melodic on ubuntu 18.04 and setting up environment tutorial along with robotic arm packages and dependencies installation 

When I tried to install ROS noetic on Ubuntu 20.04 I faced multiple issues and did not work for my virtual device. That is why I installed ROS melodic version that works well with Ubuntu 18.04. 
In this repository, the instructions and resources used to install ROS and robotic arm packeges are demonstrated.
[The order of these instructions may differ from a user to another]

### I. INSTALLING ROS MELODIC
In order to install or update any software in Ubuntu, it is common to use the terminal commands provided by the software publishers.
So, first step is **opening terminal**.
Then, following the written [Wiki Ros instructions](http://wiki.ros.org/melodic/Installation/Ubuntu) to install ROS melodic on Ubuntu which are in this way:

**Setting up source.list**
```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

```
it will ask for password, enter it and press "enter".
```
[sudo] password for device:
```

**Installing curl commands**
```
$ sudo apt install curl

```

**Setting up keys**
```
$ curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -

```

**Installing ROS** 
```
$ sudo apt update
```
Then installing Desktop-Full that contains all important libraries.
```
$ sudo apt install ros-melodic-desktop-full
```
A message saying that additional disk space is required, Do you want to continue?[y/n] will appear, enter :
```
y
```
just make sure you have enough space at least 2GB before you enter y.
if not, go to your vitual machine settings and maximize the machine's space.
The downloading process will take some time depending on internet connection.


If the downloading process got interrupted or stopped, try to use this command:
```
$ sudo apt-get install
```

**Environment setting up**
```
$ sudo rosdep init
```
it will ask for password, enter it. Then enter:
```
$ rosdep update
```
After that, add ROS environment variables to bash using:
```
$ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
```

**Dependencies and other tools installation**
```
$ sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
This step will ask requires some extra space, enter again:
```
y
```
To make sure that this tools have been installed properly use this command:
```
$ printenv | grep ROS
```
If the results did not have any errors you can proceed to next instruction, if it had issues, copy the error and search it online.

**Building catkin workspace**
```
$ pwd
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
$ source devel/setup.dash
$ echo $ROS_PACKAGE_PATH
```
Now you are done with ROS melodic installation! to make sure it is running properly try:
```
$ roscore
```

### II. ROBOT ARM PACKEGES SETUP
For Robotic Arm packeges installation I followed [Smart-methods](https://github.com/smart-methods/arduino_robot_arm/) tutorial in which was as follows:
**Dependencies installation**
these instructions will install important plugins and packeges to illustrate and controll the robotic arm, it will ask again if you agree on installing in exchange of extra space, enter y. It will ask for password too.
```
$ git clone https://github.com/smart-methods/arduino_robot_arm.git 
$ cd ~/catkin_ws
$ rosdep install --from-paths src --ignore-src -r -y
$ sudo apt-get install ros-melodic-moveit
$ sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
$ sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
$ sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
```
once installation is done, the final steps will be: 
```
$ catkin_make
$ sudo nano ~/.bashrc
```
After entering the password, bash file will appear on another terminal window, go to the bottom of the file and type: 
> source /home/yourDeviceNAme/catkin_ws/devel/setup.bash

Note that you must change the "yourDeviceName" into the name of the machine you are using to install the packeges.
press `Ctrl` + `o` to write on bash file.
press `Ctrl` + `x` to get out

Now go back to terminal, type:
```
$ source ~/.bashrc
```
To lounch Rviz and gazebo simulator run this:
```
$ roslaunch robot_arm_pkg check_motors.launch
```
Now you can control the robotic arm.

![robotic arm joint state publisher](https://user-images.githubusercontent.com/83130573/124487864-df4c3800-ddb7-11eb-9ad0-361dd248173b.PNG)
