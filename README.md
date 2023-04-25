# USER INTERFACE FOR MOVE THE ROBOT UR WITH ROS

## Prerequisites
* Ubuntu 18 or 20
* ROS - Melodic (http://wiki.ros.org/melodic/Installation/Ubuntu) or Noetic (http://wiki.ros.org/noetic/Installation/Ubuntu)

## Building UR ROS drivers

Information taken from: https://github.com/SurgicalRoboticsUMA/Universal_Robots_ROS_Driver

**Note:** The driver consists of a [C++
library](https://github.com/UniversalRobots/Universal_Robots_Client_Library) that abstracts the
robot's interfaces and a ROS driver on top of that. As the library can be built without ROS support,
it is not a catkin package and therefore requires a different treatment when being built inside the
workspace. See The alternative build method below if you'd like to build the library from source.

```bash
# source global ros
$ source /opt/ros/<your_ros_version>/setup.bash

# create a catkin workspace
$ mkdir -p catkin_ws/src && cd catkin_ws

# clone the driver
$ git clone https://github.com/UniversalRobots/Universal_Robots_ROS_Driver.git src/Universal_Robots_ROS_Driver

# clone fork of the description. This is currently necessary, until the changes are merged upstream.
$ git clone -b calibration_devel https://github.com/fmauch/universal_robot.git src/fmauch_universal_robot

# install dependencies
$ sudo apt update -qq
$ rosdep update
$ rosdep install --from-paths src --ignore-src -y

# build the workspace
$ catkin_make

# activate the workspace (ie: source it)
$ source devel/setup.bash
```
## To Launch

Before launching the node, make sure that your UR3 robot (real robot or simulator) is running, and that you have set the ip address of the robot properly in the launch file. The IP address should be the same of the one displayed in the robot console or simulator.

Dowloads the packages uma_ur_launch from https://drive.google.com/drive/folders/1ORcxtGVBTH6eXJIcqQ8fm19fdUVjTGwb?usp=share_link
and copy it in your catkin_ws/src.

Compile your workspace
```
$ catkin_make
```
For the autonomous robot
```bash
$ roslaunch uma_ur_launch ex-ur3-auto.launch 
```
For the teleoperated robot
```bash
$ roslaunch uma_ur_launch ex-ur3-teleop.launch 
```
## UR3 in the lab
The IP for the autonomous robot is: 192.168.1.20

The IP for the teleoperated robot is: 192.168.1.10
