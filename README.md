# Final Project

## Set up the working evironment

First of all, set the directory to install OpenIGTLink in your computer. These steps are taken from the following github repository: https://github.com/openigtlink/ROS-IGTL-Bridge, but are simplified here.

```bash 
$ mkdir -p ~/igtl
$ cd igtl
$ git clone https://github.com/openigtlink/OpenIGTLink.git
$ mkdir OpenIGTLink-build
$ cd OpenIGTLink-build
$ cmake -DBUILD_SHARED_LIBS:BOOL=ON ../OpenIGTLink
$ make
```

Create a working space to install the ros packages. Previously, presented:

```bash
$ mkdir -p ~/catkin_ws/src
$ cd catkin_ws
$ catkin_make
```

Now download all the files from this repository to the src folder to build the packages.

```bash
$ cd ~/catkin_ws/src
$ git clone https://github.com/mikelitu/Final-Project.git
$ cd ~/catkin_ws
$ catkin_make --cmake-args -DOpenIGTLink_DIR:PATH=~/igtl/OpenIGTLink-build
```

## Launching the simulation

To check if everything was correctly build, launch the demo for the universal robot:

```bash
$ cd ~/catkin_ws
$ source devel/setup.bash
$ roslaunch ismr19_moveit demo.launch
```

## Launching the connection
The rviz node containing the universal should be shown. Now setup the rest of the components to stablish the connection between Slicer and ROS. Open two new terminals and type the following lines

```bash
$ cd ~/catkin_ws
$ source devel/setup.bash
$ rosrun ismr19_control igtl_exporter.py
```

```bash
$ cd ~/catkin_ws
$ source devel/setup.bash
$ roslaunch ros_igtl_bridge bridge.launch
```

Now the bridge between ROS and Slicer should be ON in the IGTLink extension for Slicer.
