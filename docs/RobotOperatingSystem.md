# Robot Operating System

## ROS Noetic

ROS Noetic is the last version of ROS 1 which is soon reaching its EOL. Now the importance of this version is the relative ease in use. All the packages are maintained well and can be used easily and quickly. The build and runtime are relatively lower and easier to debug and resolve. 

For drones, the SITL using Ardupilot is much more easier in ROS Noetic, in comparison to ROS 2. This is due to a very established MAVROS package which utilizes the MAVLink protocol to communicate with the flight controller. This communication can be setup, by using a launch file called apm.launch.

## ROS 2 Humble
ROS 2 is the newer version of the Robot Operating System, which uses a completely different communication protocol underneath. It uses something called DDS. Apart from these changes, it uses a different build system to build its package (ament_cmake, colcon), and also the syntax has also changed. The version is to give much more flexibility to the lifecycle management of the node. If all this sounds like gibberish and it is something you are interested in exploring, the links to the associated concepts will be provided. 


## Differences between the both while implementation 
The main difference that you can catch while looking is the change in the way the packages are built. ROS 2 uses another build system for CMake called ament_cmake. The command to build the package is ``colcon build``, as opposed to ``catkin build`` in Noetic. The syntax has also changed quite a lot, talking purely from the perspective of C++ code. ROS 2 uses a lot of C++ 11 features.

ROS 2 supports multiple nodes running in parallel, allowing to leverage multi-core processors, which is a bit better than ROS 1. QoS allows to configure the data flow, dictating sending and recieving messages. It includes message reliability, deadline, priority, which ensures message with higher priority can be delivered on time. [This](http://design.ros2.org/articles/changes.html#:~:text=ROS%201%20uses%20a%20custom,based%20on%20the%20DDS%20standard.) link will provide a detailed, point by point improvements/differences between ROS 1 and ROS 2.


### Bagfile Problem
ROS 2 is not backwards compatible due to a lot of fundamental changes in its construction. Compared to ROS 1, which has its own serialisation format, ROS 2 rosbags offer more flexibilty. The main effect of the ROS 1 to ROS 2 rosbag format changes is that tools for ROS 1 bags may not be compatible with ROS 2 rosbags, which could have an influence on developer processes. 

The same rosbags that work in ROS Noetic, does not work with any ROS 2 option. The tools used to handle the data from the bagfiles are different, due to the different serialization format. 

## Future Work Suggestions

1. For the bagfile problem, there are solutions with ROS 2 Foxy and ROS Noetic. To convert the bagfile format use one of these method and create a docker based application to convert ROS 1 bagfiles to ROS 2 and then test it with latest ROS 2 distro's such as Humble and Iron.

2. Creating plugins for RViz for Waypoint navigation taking inspiration from the CTU-MRS stack (developed using ROS Noetic) for ROS 2 systems. [RViz Aerial Plugins](https://github.com/osrf/rviz_aerial_plugins) can be used as the base to start with.

3. Configuring a forest based 3D environment in Gazebo integrated with the ArduPilot SITL for ROS 2, for testing the sensor suite and navigation algorithms. 

4. Developing localization and planning algorithms based on the voxelization methods chosen. Complete utilization of 3D Occupancy Grids.

5. Localization method using monocular camera sensors, with LiDAR generated maps.