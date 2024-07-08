## Introduction

A problem we as intellectuals face is the conundrum whether the chicken came first or the egg. The chicken lays the egg, but the chicken must have come out of some egg, but where is that egg from. No idea. Now why this problem is relevant

Consider a robot, something like Wall-E for imagination purposes, is exploring an unknown scrap yard. It has to  

- Build a map: Make a representation of the surroundings, landmarks and other useful places of interest and importance.  
- Localise itself: Locate itself within the environment.

Well, the problem is not as easy as it seems. These tasks are actually dependent on each other.
To accurately build a map of the environment, the robot needs to know where it is in the environment. (Where am I headed to? How far have I come?)
To locate itself in the environment, it needs a reference map. (Where are the cones and tables, wrt to where I am?)

So, this is a cyclic dependency problem, just like the chicken and egg problem. Luckily the problem has been solved, but now we have to understand how it is solved. To understand this, fundamental and in depth knowledge in calculus, computer vision, geometry, stochastic processes, optimization of functions and many more. The documentation is to make sure that an intuitive understanding can be provided to the concepts and provide resources to go ahead with in-depth reading and understanding.

## Simultaneous Localization and Mapping

The problem of localization and mapping can be solved in many different ways which is evident from a lot of different techniques of SLAM. The overall gist is as the follows:

Use a prior information: Even without a map, external sensors can be used to estimate the initial position and provide estimate of movement
The robot uses sensors such as LiDAR, camera’s, IMU’s or ultrasonic sensors. The data can be used to identify landmarks or distinct features. 
Use the initial movement and the data from the sensor to generate a map, which optimises the more you explore and gather data.
Gradually as the map gets more detailed, the robot can use this map to localise itself in the environment and determine its position.
More precise position information can also improve the quality of the map in terms of accuracy.

This continuous loop of exploration, measurement and refinement is a gist of what SLAM does in order to solve the problem. Within these steps there are a lot of components that work in tandem which gives us this output. Depending on the sensor and the method of SLAM chosen, this can vary. Nevertheless the underlying fundamental problem and logic are the same.

[Fundamentals of SLAM](https://drive.google.com/drive/folders/1EflI2OfYi6TXw80cJJ9HhC6RQERBondZ?usp=drive_link) is the drive folder that contains resources for different concepts which will be briefly explained in the further sections. The folder SLAM Fundamentals contains all the resources and links to YouTube playlists to understand the basics of SLAM.

## Different Type of SLAM

At a rudimentary standpoint, let's classify SLAM based on the sensor used. There are SLAM methods that use LiDAR sensors and there are others that use camera sensors, therefore called Visual SLAM. 

It can be said that fundamentally the sensor that is used to perceive depth is different in each case. The basic overall flow for SLAM is very similar, but depending on the sensor used there are workarounds done to make it work.

A very good intuitive understanding about the fundamentals of SLAM can be found in the book [SLAM for Dummies](https://drive.google.com/file/d/1sS-y-YJMqx7L7xerzcybDXIxsfWAPmxT/view?usp=sharing ), which explains concepts in the LiDAR based SLAM approach. 

There will also be a dedicated section to visual SLAM, its classification and its fundamentals, since more in-depth research is done in that space.

A brief of what we classify as the frontend and the backend of a SLAM method will be given in the next few sections.

## Components of SLAM

SLAM on a very broad basis can be split into frontend and backend. The frontend focuses on collecting anchor points or landmarks to be tracked for optimization, which will be done in the backend of the algorithm. Overall, SLAM's frontend-backend design allows for quick sensor data processing, reliable feature extraction and tracking, and continuous map and robot pose refining. This enables robots to navigate unknown regions while simultaneously creating a map of their surroundings in real time.

### Frontend

Frontend of the algorithm purely handles the raw data from the sensors. These may involve:

- Preprocessing: This involves synchronization of data from multiple sensors (if involved), and correcting for distortions in the sensor data. 
- Feature or Points extraction: Identifying landmarks or features from the perception data. These can be corners, edges, specific patterns (Indirect) or points and intensity values (Direct). 
- Data Association: Creating initial correspondences between features observed in one sensor frame and those observed in succeeding frames. This entails identifying probable matches that could represent the same landmark or point in the environment from various perspectives.

### Backend

Backend uses the feature correspondence from the frontend of the algorithm and optimize to build a robust representation of the environment and estimate the pose of the sensor.

- Pose Estimation: Based on sensor data, feature correspondences, and the current map, the backend calculates the robot's most likely pose (position and orientation) for each sensor frame. This entails addressing optimisation challenges to reduce the discrepancy between observed and expected sensor measurements. Adding new features to the map if they are consistently tracked and deemed reliable. Removing outdated information from the map to maintain accuracy and efficiency.

- Data Association Refinement: The backend refines the frontend's initial feature associations. It uses techniques such as outlier rejection and statistical analysis to ensure that features are accurately matched between sensor frames. This reduces false positives and improves the overall accuracy of pose estimation and mapping.

- Loop Closure Detection: In some SLAM techniques, the backend can identify loops. This refers to scenarios in which the robot returns to a previously investigated location. Loop closure aids in detecting and correcting cumulative errors in map and robot pose estimation over time. By recognising loop closures, the algorithm can ensure consistency between previous and current observations, resulting in a more scale accurate global map.


## LiDaR Odometry and Mapping (LOAM)

LOAM is a method of LiDAR SLAM, which excels at real-time processing of LiDAR data and can generate a high-resolution 3D map. The actual idea of coming up with this method is the fundamental decomposition of the SLAM problem. One algorithm estimates the lidar's velocity by performing odometry with a high frequency but low fidelity. For the purpose of fine matching and point cloud registration, a different algorithm operates at a frequency that is an order of a magnitude lower.

The paper [LOAM: Lidar Odometry and Mapping in Real-time](https://www.ri.cmu.edu/pub_files/2014/7/Ji_LidarMapping_RSS2014_v8.pdf) provides an insight into the basic structure and capabilities of the algorithm. Additional experimentation had been done and there are multiple modification done on this algorithm and have vaious spinoff implementations. One such implementation is [SLOAM](https://drive.google.com/file/d/1K9KLpPvzVBA3ko5MT9YJObHvUqvCKcmy/view?usp=sharing) by UPenn.


## Resources and References

 

[SLAM for Dummies](https://drive.google.com/file/d/1r5Lc7DGS1lvqQ407OQD8CCkfvG5BiJJl/view?usp=drive_link)

[Cyril Stachniss Fundamentals of SLAM](https://youtube.com/playlist?list=PLgnQpQtFTOGQrZ4O5QzbIHgl3b1JHimN_)

[SLAM Resources ordered](https://github.com/ckddls1321/SLAM_Resources) is a github link to all the resources regarding SLAM in a definite and sorted order.

