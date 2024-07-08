# Perception and Vision

Perception is the fundamental concept of how a robot can understand the surrounding environment to derive a set of actions, which then further dictates the flow of control. There are various sensors that are used and fused to make the robot aware of its surroundings and the changes by its actions. The two important ones we’ll be looking into will be the Camera sensor and LiDAR sensor.
## Camera Sensors
Camera sensor is a primary sensor used in perception. It takes in light through the opening of the shutter of the sensor, and as the light enters, it is projected onto the light receptors called photosites. A very simple and fundamental model of a camera is the pinhole camera. Here the pinhole acts as a single photosite in a camera sensor, and the inverted image on the flat surface is basically the light information captured by the sensor.

### Types of Camera Sensors
Strictly speaking wrt robot perception there are three main camera sensors that are being used, these are:

*  Monocular: As the name suggests, it uses a single lens to capture image and videos.
*  Stereo: Stereo uses two or more image sensors, which allows it to simulate human binocular vision
*  RGBD: It is a type of depth camera that can output the RGB and Depth value as the output in real time. 

These camera sensors are fundamentally different in the way they provide the data for use to complete tasks. The algorithms used for perception therefore also differ depending on the data it recieves.  In Visual SLAM/ Visual Odometry, there are distinct SLAM/ Odometry methods which utilise Monocular, Stereo and RGB-D data. 

## Camera Calibration

Imagine we have a checkerboard and we take an image of it using a camera. Due to the imperfections of the camera sensor, the image might appear warped. The warped image can be fixed using the camera parameters which we obtain using camera calibration. One of the most popular method of camera calibration is Zhang’s camera calibration method. This method helps you understand how the camera "sees" the checkerboard, fixing any distortions and allowing you to make accurate measurements from the image. Here's a breakdown:
The most important component is the checkerboard. It offers a distinct pattern with corners that are simple to recognise (intersections of black and white squares).

- Taking Pictures: You capture the checkerboard in many images from different angles. The more pictures, the better the calibration. 

- Software Analysis: The photos that are taken are examined by software. It locates the checkerboard corners in every image, effectively producing a set of data points at the locations of the corners.

- The actual dimensions and distances between the checkerboard squares are known to us. The "ground truth" data is essential. 

- The program makes a comparison between the dimensions of the checkerboard that are known and the way the camera captured them in the photographs. This shows the distortions from the imperfect camera lens.

- Creating a Model: The programme creates a mathematical model that explains how the image is projected onto the camera sensor from the real world—the checkerboard. This model considers factors like:
    - Focal Length: It is the distance between the camera sensor and the optical centre of the lens, where the light information is recorded. 
    - Distortion: The way a lens causes straight lines in the actual world to look bent in an image.
    - Center of Projection: The principal point where light rays converge on the sensor.

Consider it this way: In essence, what you're doing here is mapping out the real world (checkerboard) to the distorted picture (image) produced by the camera.This map allows you to interpret the image with greater accuracy. 

Some of the research that was done for Camera Calibration is documented in [Research in Camera Calibration folder](https://drive.google.com/drive/folders/1NxsEjRYz0YHOqGlHd5teUmEvTLV3bOyM?usp=drive_link)
### Tutorial using MATLAB app for Camera Calibration
[Zhang's Calibration method with Tutorial](https://drive.google.com/file/d/1n3oWYMgarv50yofy9DA8FdWqgZquzT5d/view?usp=drive_link)

### Camera Models used for SFM and SLAM

The camera model will help in undistorting the images taken, which can help massively in undistorting the images. Moreover they are mathematical representations of the complexities that accompany with a real camera. Camera models such as pinhole, FOV, Rad-Tan, and Equidistant offer varied degrees of complexity in representing the relationship between the 3D world and a camera's 2D image. Understanding their capabilities and limitations is critical for jobs involving SfM, SLAM, and other applications that require precise image interpretation.

Pinhole Camera: Assumes a straight line projection between a 3D point in the world frame to a correcponding 2D point in the image plane. This is the most fundamental model.

FOV Model: Extends the pinhole camera by including the field of view of the camera, ie. defines the angular extent of the scene captured by the image sensor.

Radial-Tangential Model: This model improves the pinhole model by incorporating radial distortion generated by the camera lens. Lenses frequently bend light slightly, causing straight lines in the actual world to look curved in the image, particularly near edges. These are caused by the imperfections in the lens manufacturing. 

Equidistant Model: This model is specifically designed for fisheye lenses, which capture an extremely wide field of view (often close to 180 degrees). Straight lines in a fisheye image become more bent as they go out from the image centre. The equidistant model maps 3D locations onto the picture plane using a precise mathematical model, which accounts for the high distortion.

## LiDAR 

Light Detection And Ranging (LiDAR) is a sensor that uses light pulses, which reflects off surfaces and return to the sensor. It uses the time taken for each pulse to return to the sensor to calculate the distance. LiDAR sensor is usually used in robotics to obtain dense point cloud of the surrounding, which is then registered and corrected with IMU data using SLAM or SLOAM methods. The maps generated can be used for providing spatial information in 3-dimensions to UAVs whose DoF is 6. 
Some of the different types of LiDAR sensor available are Mechanical, Hybrid Solid State and  Optical Phased Array. You can use this [link](https://www.dfrobot.com/blog-1643.html) to understand more about the different types of LiDAR sensor, based on its construction. 

## Datasets for Perception


It is always best to use well known benchmark datasets to evaluate and understand perception algorithms. Even when the sensor is not available physically, we can get live time-synchronised data, with the help of bagfiles as well.

A good example for this is the treescopes dataset. It is an under the canopy forest dataset, taken using UAV’s and mobile platforms. It boasts a very advanced sensor suite and the data has been processed using a LIO method to fuse the inertial and LiDAR data to give an accurate registered pointcloud, and further processed using RangeNet++ for bark and ground plane identification. Another such dataset is the M3ED dataset, which contains data from multiple kinds of sensors like LiDARs, event camera’s, RTK-GPS, IMU and stereo cameras. 

For Visual SLAM and Visual Odometry there are datasets which contain images in frame by frame manner, along with the camera intrinsic. Some of the datasets are Monocular VO by TUM and EuRoC MAV dataset by ETH Zurich. For the testing of DSO, LDSO and SVO, these were the datasets that were being used.


## Resources and References

