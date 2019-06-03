---
layout: post
title: ROS Learning
category: ROS
tags: [Education, Opioions]
---
回顾在DJI学习的ROS知识。

<p align="right">
Author：Richard 
</p>

<p align="right">
Github:
<a href="https://github.com/CheKaiWei/ARM-Programming/tree/master/int"> INT</a>
</p>

## Environment
Ubuntu18  
ROS Melodic 

## Source
[ROS](http://www.ros.org/)  
[ROS Tutorials](http://wiki.ros.org/ROS/Tutorials)


## Configuring ROS Environment
```bash
$ source /opt/ros/melodic /setup.bash
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
```
```
$ source devel/setup.bash
$ echo $ROS_PACKAGE_PATH
/home/youruser/catkin_ws/src:/opt/ros/kinetic/share
```

## ROS Filesystem
### Structure
```bash
workspace_folder/        -- WORKSPACE
  src/                   -- SOURCE SPACE
    CMakeLists.txt       -- 'Toplevel' CMake file, provided by catkin
    package_1/
      CMakeLists.txt     -- CMakeLists.txt file for package_1
      package.xml        -- Package manifest for package_1
    ...
    package_n/
      CMakeLists.txt     -- CMakeLists.txt file for package_n
      package.xml        -- Package manifest for package_n
```

### Filesystem Tools
```bash
rospack = ros + pack(age)
roscd = ros + cd
rosls = ros + ls
```

```bash
$ rospack find [package_name]
$ rospack find roscpp
YOUR_INSTALL_PATH/share/roscpp

$ roscd [locationname[/subdir]]
$ roscd roscpp
$ pwd
YOUR_INSTALL_PATH/share/roscpp

$ echo $ROS_PACKAGE_PATH
/opt/ros/kinetic/base/install/share

$ roscd roscpp/cmake
$ pwd
YOUR_INSTALL_PATH/share/roscpp/cmake

$ roscd log

$ rosls [locationname[/subdir]]
$ rosls roscpp_tutorials
cmake launch package.xml  srv
```

## Package


### Create Package
```bash
$ cd ~/catkin_ws/src
$ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```

### Build
```bash
$ cd ~/catkin_ws
$ catkin_make
$ . ~/catkin_ws/devel/setup.bash
```

### Package Dependencies
```bash
$ rospack depends1 beginner_tutorials 
$ roscd beginner_tutorials
$ cat package.xml
$ rospack depends1 rospy
$ rospack depends beginner_tutorials
```

### Customizing the package.xml
```bash

```

### Customizing the CMakeLists.txt
```bash

```


## ROS Nodes
### roscore
```bash
$ roscore
```

### rosnode
```bash
$ rosnode list
$ rosnode info /rosout
```

```bash
$ rosnode list
/rosout
$ rosnode info /rosout
------------------------------------------------------------------------
Node [/rosout]
Publications:
 * /rosout_agg [rosgraph_msgs/Log]

Subscriptions:
 * /rosout [unknown type]

Services:
 * /rosout/get_loggers
 * /rosout/set_logger_level

contacting node http://machine_name:54614/ ...
Pid: 5092

$ rosnode ping turtlesim_node

```

### rosrun
```bash
$ rosrun turtlesim turtlesim_node
```
```bash
$ rosrun [package_name] [node_name]
$ rosrun turtlesim turtlesim_node
$ rosrun turtlesim turtle_teleop_key
```

## ROS Topics

### rostopic
```bash
rostopic bw     display bandwidth used by topic
rostopic echo   print messages to screen
rostopic hz     display publishing rate of topic    
rostopic list   print information about active topics
rostopic pub    publish data to topic
rostopic type   print topic type
```

### rostopic echo
```bash
$ rostopic echo [topic]
$ rostopic echo /turtle1/cmd_vel
$ rostopic list -h
  -b BAGFILE, --bag=BAGFILE
                        list topics in .bag file
  -v, --verbose         list full details about each topic
  -p                    list only publishers
  -s                    list only subscribers
$ rostopic list -v
```

###  rqt
```bash
$ sudo apt-get install ros-<distro>-rqt
$ sudo apt-get install ros-<distro>-rqt-common-plugins
$ rosrun rqt_graph rqt_graph
```

## ROS Messages
### rostopic type
```bash
$ rostopic type [topic]
$ rostopic type /turtle1/cmd_vel
geometry_msgs/Twist
```

### rosmsg show
```bash
$ rosmsg show geometry_msgs/Twist
geometry_msgs/Vector3 linear
  float64 x
  float64 y
  float64 z
geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z
```
### rostopic pub
```bash
rostopic pub [topic] [msg_type] [args]
rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, 1.8]'
```

### rostopic hz
rostopic hz reports the rate at which data is published.
```bash
$ rostopic hz [topic]
$ rostopic hz /turtle1/pose
subscribed to [/turtle1/pose]
average rate: 59.354
        min: 0.005s max: 0.027s std dev: 0.00284s window: 58
average rate: 59.459
```

### rqt_plot
```bash
$ rosrun rqt_plot rqt_plot
```