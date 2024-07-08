# VI-SLAM

## Visual SLAM

Visual SLAM is a type of SLAM that used a camera in its frontend to extract points and landmarks. There are different types of V-SLAM based on the camera sensor that is being used. The SLAM method that uses a single camera is called a Monocular SLAM. The cost of a monocular camera sensor is low and hence it is a very popular method amongst researchers. A photo is essentially a projection of a scene onto a camera’s imaging plane. A monocular camera's image is a 2D projection of 3D space. To restore the 3D structure, alter the camera's view angle. Monocular SLAM follows the same principle. We move the camera and estimate its motion, as well as the distances and sizes of the objects in the image, so determining the scene's structure.  

In monocular SLAM, depth can only be estimated by translational movement, and the true scale cannot be determined. These two factors potentially provide significant obstacles when implementing monocular SLAM in real-world applications. So, to achieve real-scaled depth, we begin to use stereo and RGB-D cameras. 

A stereo camera consists of two synchronised monocular cameras separated by a specified distance, called the baseline. Because the actual distance to the baseline is known, we can calculate each pixel's 3D position in a manner similar to human vision.  The downside of stereo cameras or multi-camera systems is that the configuration and calibration processes are complex. Their depth range and accuracy are constrained by the baseline length and camera resolution. Furthermore, stereo matching and disparity calculation use a lot of processing resources and typically require GPU or FPGA acceleration to build real-time depth maps.

Depth cameras, commonly referred to as RGB-D cameras, have become increasingly popular since 2010. Similar to laser scanners, RGB-D cameras use infrared light structure or Time-of-Flight (ToF) principles to determine the distance between objects and the camera by actively generating light and receiving the returned light. The distance is not calculated on software, like for example using a stereo camera, but by using physical sensors instead which reduces the computational power required. But for SLAM purposes, RGB-D sensors doesnt prove effective, and hence are mainly used for Indoor purposes.

In the subsequent sections, there will be explainations about Monocular SLAM, and within Monocular SLAM, Direct and Indirect Methods.

[A Comprehensive Survey on SLAM Algorithms](https://drive.google.com/file/d/1VPuuPsmYZ7gOq7QFYedpsPrW8LOpjGo1/view?usp=drive_link) is a survey paper on different open-source SLAM algorithms, which can give you a basic idea of the different methods available. Some of the other popular methods are listed below

- [LSD SLAM](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=ca69cb679a3599aea3350d2b7872dbd669f43612)

- [PTAM](https://drive.google.com/file/d/17VnUfP5zfqp0z7ZRoCJFGjDlO3Ff2aVl/view?usp=drive_link)

- [DTAM](https://drive.google.com/file/d/1YVvcwr-7V2wzTVnl_ZSToI6Uv5JzGdBI/view?usp=drive_link)

## Visual Odometry

Visual Odometry is a method to estimate the ego-motion of a system using only visual input. The methodology used to estimate postion and velocity using images are similar to Visual SLAM methods. The fundamental difference between the both, is the fact that V-SLAM does both localization and mapping and incorporates methods like loop-closure, sensor integration and map reusal inorder to improve the localization, which VO does not. Due to this reason, the VO algorithms run faster than SLAM, and the maps generate are error prone and tend to be less detailed.

Some popular methods are:

- [SVO-Hybrid Method](https://drive.google.com/file/d/1y1jpeNevBEO6ocO3ebj7E9T7mKq3xYmM/view?usp=drive_link)

- DSO is also another Monocular Visual Odometry method, which will be explained in detail in the [Direct Sparse Odometry](https://dfx-rick.github.io/test-site/DirectSparseOdometry/) section.

## Direct vs Indirect

Indirect methods relies on extracting and tracking features (e.g., corners, edges) from consecutive image frames. The main challenge of VO/VSLAM is estimating camera motion from nearby images. However, the image itself is a numerical matrix that encodes brightness (intensity) and colour. The integers in the matrix are abstract, making it difficult to calculate motion directly at the pixel level. Hence, it is more convenient to perform the extraction of features which will remain costly even when the camera moves slightly. After this, it then matches corresponding features across frames to establish geometric relationships.Using these relationships and camera models the camera motion is estimated and concurrently reconstructs 3D scene structure. Some examples of features that can be extracted are SIFT and ORB. 

- [ORB-SLAM](https://drive.google.com/file/d/1jvuiIrJEwVmROoobQWO3fRpeu0KdtUhg/view?usp=drive_link) is a very prominent SLAM method that uses feature extraction from images.
- [VINS Mono](https://ieeexplore.ieee.org/document/8421746/?arnumber=8421746&source=authoralert) uses Harris Corner features and then uses them to perform the KLT Tracker to track the points across the frames.

Some of the other Indirect Methods are listed below:

- [Kimera](https://arxiv.org/pdf/1910.02490)
- [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion)
- [OKVIS](https://github.com/ethz-asl/okvis)
- [ORB-SLAM 2](https://drive.google.com/file/d/1v_V2ypbmJQwEGxVlfSFjFH7iifloU746/view?usp=drive_link)

But unfortunately, feature based methods require really good methods for feature detection and tracking, which can be computationally expensive. The method also proves ineffective in environments where there are repeated features, like forests or blank walls. The feature technique does not make advantage of all available information. An image has hundreds of thousands of pixels, but only a few hundred feature points. Using simply feature points discards the majority of potentially important image information.


Direct methods on the other hand operates directly on the image's intensity values (pixels). A corresponding reprojection error function is formulated. This error function is further optimized to get the camera pose estimation. Direct Sparse Odometry is a direct method, that has been explained in detail. As a matter of fact, a lot of the direct methods have very common base logic. 

Some other Direct Methods are

- [LSD SLAM](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=ca69cb679a3599aea3350d2b7872dbd669f43612)
- [Direct Sparse Odometry](https://dfx-rick.github.io/test-site/DirectSparseOdometry/)
- [ROVIO](https://github.com/ethz-asl/rovio?tab=readme-ov-file)

[Direct Methods](https://drive.google.com/drive/folders/1hswq3APOHAy0uVBZ28nA7YARm3MZYCEy?usp=drive_link) in the [Fundamentals of SLAM](https://drive.google.com/drive/folders/1EflI2OfYi6TXw80cJJ9HhC6RQERBondZ?usp=drive_link) folder contains the papers that explain the fundamentals of Direct SLAM with camera's with related concepts.

## Resources and References

[SLAMBook](https://drive.google.com/file/d/1r5Lc7DGS1lvqQ407OQD8CCkfvG5BiJJl/view?usp=drive_link) is an excellent resource for beginners and veterans alike. The book explains the math and the intricacies behind the concepts that go into building a visual SLAM method. Anyone who wants to learn about Visual SLAM have to go through this book to understand the concepts at a very rudimentary level.

[Visual Navigation for Flying Robots](https://youtube.com/playlist?list=PLTBdjV_4f-EKeki5ps2WHqJqyQvxls4ha) consists of video lectures that explains all the concepts pertaining to the navigation of a robot, from mapping, localization to path planning.