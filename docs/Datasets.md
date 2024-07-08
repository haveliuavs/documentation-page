## Datasets for Perception

It is always best to use well known benchmark datasets to evaluate and understand perception algorithms. Even when the sensor is not available physically, we can get live time-synchronised data, with the help of bagfiles as well.

A good example for this is the treescopes dataset. It is an under the canopy forest dataset, taken using UAV’s and mobile platforms. It boasts a very advanced sensor suite and the data has been processed using a LIO method to fuse the inertial and LiDAR data to give an accurate registered pointcloud, and further processed using RangeNet++ for bark and ground plane identification. Another such dataset is the M3ED dataset, which contains data from multiple kinds of sensors like LiDARs, event camera’s, RTK-GPS, IMU and stereo cameras. 

For Visual SLAM and Visual Odometry there are datasets which contain images in frame by frame manner, along with the camera intrinsic. Some of the datasets are Monocular VO by TUM and EuRoC MAV dataset by ETH Zurich. For the testing of DSO, LDSO and SVO, these were the datasets that were being used.

## Monocular VO by TUM

Monocular Visual Odometry is a dataset for testing and benchmarking Visual Odometry and Monocular SLAM methods. It contains aboout 50 sequences recorded across different type of environments. The speciality of the dataset is that it provides the photometric calibration of the camera, and also points to a method to photometrically calibrate images. When it comes to direct method, photometric calibration is an absolute game-changer and have proven to increase performance, especially in the case of Direct Sparse Odometry. 

The structure of the dataset provided is as followed:

- images.zip :  Contains the video in a frame by frame JPEG or PNG file
- camera.txt : Contains the intrinsic parameters of the camera, which can be obtained through calibration
- pcalib.txt : Contains a single row with 256 values, mapping [0..255] to the respective irradiance value, i.e. containing the _discretized inverse response function_.
- times.txt  : Contains exposure times of each frame as given by the sensor
- vignette.png : Contains the vignette as pixel wise attenuation factors. 
- groundtruthSync.txt: Contains the time synchronizeed ground truth information for each camera pose, corresponding to the image timestamps.

A direct photometric calibration method is being shared by the same research group. [Online Photometric Calibration](https://drive.google.com/file/d/1I6qHwjdz8MiKHd_BqSSIGkKn1UV9v762/view?usp=drive_link) uses a Levenberg-Marquardt based optimization after modelling the vignetting and response functions. This can be modified either to be run with video sequences or with live camera. Depending on the mode of calibration chosen, we can save the inverse response function and the vignetting factors or can directly wire it to the VO or SLAM algorithm. 
## EuRoC MAV by ETH Zurich

The EuRoC dataset includes synchronised timestamped data from a stereo camera system and an IMU (Inertial Measurement Unit) in a variety of demanding outdoor and interior conditions. The structure of the dataset is as follows:

- images.zip A compressed archive of grayscale photos collected by the stereo camera system. The archive usually has two subfolders (left and right) for the left and right camera photos, respectively.
- imuX.txt (multiple files): Text files containing synchronised Inertial Measurement Unit (IMU) data. These files contain measurements such as accelerometer, gyroscope, and sometimes barometer readings at timestamps that match the camera photos.
- groundtruth.txt: A text file holding the ground truth information for each camera pose (position and orientation) during the recording sequence. This information is often delivered at timestamps that are consistent with the image and IMU data.

Note that some versions might include additional data files, such as calibration files for the camera system or IMU. These files are essential for correcting sensor distortions and ensuring accurate measurements. In the version we used this was not in a usable format for DSO, therefore we had to convert the parameters had to converted to .txt format and with the right distortion parameters. While running it for benchmarking for DSO, only one of the files out of the left and right images were used.  

## Creating a custom dataset for Visual Odometry/SLAM

Custom dataset can be created in the MonoVO format, which is easier to run with different algorithms. All you need is the video of the environment using a monocular camera. The calibration of the camera is needed for the pose estimation and mapping. The K matrix is considered the geometric calibration of the camera. The K matrix can be obtained by using Zhang's calibration, which can be obtained from the MATLAB tutorial provided. Using the values create the camera.txt files in the format as given by [this](https://github.com/JakobEngel/dso/blob/2c30ab44b3804d9e507ba9221dbd9f5637491f12/README.md#geometric-calibration-file.). 

It is always preferred to have the photometric calibration files as well. These are the pcalib.txt and the vignette.png files. For the algorithm to work with photometric parameters both these files have to be provided. If the exposure times can be found with the timestamp and the frame values, then the [mono-dataset code](https://github.com/tum-vision/mono_dataset_code) can be used.

If not the files can be generated by using the [online photometric calibration code](https://github.com/tum-vision/online_photometric_calibration), just by sending in the camera.txt files. When passing the parameters make sure to send the resolution values, so that the vignette image is in the same resolution as the feed. [Document 1.1](https://docs.google.com/document/d/1KuTvh2p6CwSN_qvg2MAlSIXOvKzrUPpUdWphqJ9lsBc/edit?usp=sharing) elaborates on the use of the above. 

## Treescopes

The Treescope dataset, developed by the University of Pennsylvania, provides data for robotic precision agricultural and forestry operations, notably tree counting and mapping. The Treescope dataset seeks to give academics and developers with resources that:

- Develop and refine algorithms for robotic tree counting and mapping: The dataset provides high-quality LiDAR data with ground truth labels, enabling researchers to train and evaluate algorithms for automated tree detection and estimate of tree metrics including position, height, and diameter.

- Advance LiDAR-based SLAM (Simultaneous Localization and Mapping) in agricultural settings: The dataset can be used to create SLAM algorithms that work well in orchards and woods, where typical visual SLAM approaches may fail due to a lack of visual cues.

- Benchmarking robotic system performance in precision agriculture: By providing a standardised dataset, researchers may evaluate the performance of various robotic platforms and algorithms for tree management activities in agricultural settings.


The dataset can be classified into two categories:

1. Processed data: This category includes ROS bags (Robot Operating System message format), which contain:

    -   Ground-truth LiDAR odometry: Precise information about the robot's movement derived from LiDAR data and potentially adjusted with other sensors (IMU, GPS).
    -   Velocity-corrected point cloud frames are 3D points that reflect the environment collected by the LiDAR sensor and have been corrected for sensor motion to increase accuracy.
    -  Semantically segmented point clouds: The point cloud data is further classified, with points labelled as being on the ground, tree stems, or in other relevant categories. This segmentation is carried out utilising a trained deep learning network RangeNet++.

2. Raw Data: This category includes the unprocessed sensor data acquired during the recordings.

    - ROS bags may contain raw LiDAR data, IMU (Inertial Measurement Unit) data, RGB-D camera data (colour image with depth information).
    - Sensor Metadata: Separate files containing information about the sensor models, calibration parameters, and other details needed to analyse the raw sensor data.

## Resources and Further work

1.  [Awesome SLAM datasets](https://github.com/youngguncho/awesome-slam-datasets) is a github 1. page, which has ordered different datasets that can be used to test SLAM algorithms. It has even ordered datasets based on the environments it provides.

2.  [Mapping Quality Evaluation of Monocular SLAM solutions for Micro Aerial Vehicles](https://d-nb.info/1201091020/34) 
    
    1.  [Implement Instructions for custom dataset with LSD-SLAM, ORB-SLAM2, and LDSO](https://github.com/jwangjie/Mapping-ARDrone/tree/master)

3.  [Step by Step Procedure to make the Trajectory Analysis Work](https://docs.google.com/document/d/1BPd35Z0O4dz2GUDv9r9lGRElgTcY1jWWGsgtxDiZQb8/edit?usp=sharing) will help in setting up a basic comparison and plots for understanding the performance.

