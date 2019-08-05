# A Gentle Introduction to ROS
## Chapter 1: Introduction
meta-operating system
* Distributed Computation
communication between multiple processes that may or may not live on the same  computer
* Software Reuse
ROS’s message passing interface
* Rapid Testing
simulator
rosbag
## Chapter 2: Getting Started
On Ubuntu, `rosdep` acts as a front end to `apt-get`
`rosinstall` install ROS software from source

`setup.bash` to set environment variables

to see the environment variables `export | grep ROS`

to run the `setup.bash` script automatically, then edit the file named `.bashrc`

**Packages**
`rospack list`
Each package is defined by a manifest, which is a file called `package.xml`: name, version, maintainer, and dependencies.
( Any directory that ROS can find that contains a file named package.xml is a package directory )

compiled executables are not stored in the package directory, but in `/opt/ros/distribution/lib`

to find the directory, `rospack find package-name`

To view the files in a package directory: `rosls package-name`

to go to a package directory: `roscd package-name`

**The Master**
`roscore`
nodes do not attempt to reconnect if that connection fails later on
**Nodes**
`rosrun package-name executable-name`
`rosnode list`
The `/rosout` node is a special node that is started automatically by roscore. 
The leading / in the name /rosout indicates that this node’s name is in the global namespace

**node names are not necessarily the same as the names of the executables underlying those nodes**
`rosrun package-name executable-name __name:=node-name`

to see topics and services, pid and connections: `rosnode info node-name`

to kill a node: `rosnode kill node-name`
connections reestablished when the node restarts

to remove dead nodes from the list: `rosnode cleanup`

**Topics and Messages**
* publish messages on the appropriate topics
* subscribe to the topic or topics that it’s interested in
* The ROS master takes care of ensuring that publishers and subscribers can find each other

`rqt_graph`

**Messages and Message Types**
`rostopic list`
`rostopic echo topic-name`

Measuring publication rates:
```
rostopic hz topic-name
rostopic bw topic-name

```
`rostopic info topic-name`
shows the message type of that topic

`rosmsg show message-type-name`
the format is a list of fields
composite field
```
geometry_msgs/Vector3 linear
    float64 x
    float64 y
    float64 z
geometry_msgs/Vector3 angular
    float64 x
    float64 y
    float64 z
```


Error Checking: `roswtf`

## Chapter 3: Writing ROS Programs

create package:
`catkin_create_pkg package-name`
creates two configuration files inside that directory:
* CMakeLists.txt
* package.xml

## Chapter 4: Log Messages
**Severity Levels:**
* DEBUG: ROS_DEBUG_STREAM(message)
* INFO: ROS_INFO_STREAM(message)
* WARN: ROS_WARN_STREAM(message)
* ERROR: ROS_ERROR_STREAM(message)
* FATAL: ROS_FATAL_STREAM(message);
