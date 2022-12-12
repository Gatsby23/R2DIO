# R2DIO
## Real-time, RGB-colored, Depth-Inertial Indoor Odometry for ToF RGB-D Cameras. (Intel Realsense L515 as an example)

The RGB-D camera is an essential sensor in indoor SLAM, often used on lightweight robots. However, limited by computing cost, many RGB-D SLAM systems do not fully use the multi-modal information of cameras, resulting in degeneration and low accuracy in some scenes. This letter introduces a novel, lightweight, real-time, and RGB-colored depth-inertial SLAM system for ToF RGB-D cameras. To improve robustness by using texture and structure information simultaneously, it extracts line features from RGB images and plane features from depth images efficiently based on agglomerative clustering. When matching features, the line and plane direction vector is used to filter the mismatching and enhance real-time. The IMU measurements are used to predict the poses and are tightly coupled in the system by pre-integration. Finally, the system estimates the odometry and builds dense, RGB-colored maps with the following constraints: line and plane matching constraints, IMU pre-integration constraints, and historical odometry constraints. We demonstrate the accuracy and efficiency of R2DIO in the experiments. The results indicate that our system is able to locate precisely in some challenging scenes, build colorful maps and run at 30 Hz on a low-power system. 

A summary video demo can be found at [Video]() 

**Author:** Jie Xu, Harbin Institute of Technology, China

## 1. Solid-State Lidar Sensor Example
### 1.1 Scene reconstruction
<p align='center'>
<a href="https://youtu.be/Ox7yDx6JslQ">
<img width="65%" src="/img/3D_reconstruction.gif"/>
</a>
</p>

### 1.2 SFM building example
<p align='center'>
<a href="https://youtu.be/D2xt_5xm_Ew">
<img width="65%" src="/img/3DMapping.gif"/>
</a>
</p>

### 1.3 Localization and Mapping with L515
<p align='center'>
<a href="https://youtu.be/G5aruo2bSxc">
<img width="65%" src="/img/3D_SLAM.gif"/>
</a>
</p>

## 2. Prerequisites
### 2.1 **Ubuntu** and **ROS**
Ubuntu 64-bit 20.04.

ROS noetic. [ROS Installation](http://wiki.ros.org/ROS/Installation)

### 2.2. **Ceres Solver**
Follow [Ceres Installation](http://ceres-solver.org/installation.html). 

Tested with 2.0

### 2.3. **PCL**
Follow [PCL Installation](http://www.pointclouds.org/downloads/linux.html). 

Tested with 1.10 (inherent in ros)

### 2.4. **Trajectory visualization**
For visualization purpose, this package uses hector trajectory sever, you may install the package by 
```
sudo apt update
sudo apt install ros-noetic-hector-trajectory-server
```
Alternatively, you may remove the hector trajectory server node if trajectory visualization is not needed

### 2.4. **OpenCV**
Tested with 4.2.0 (inherent in ros)

## 3. Build 
### 3.1 Clone repository:
```
    cd ~/catkin_ws/src
    git clone https://github.com/jiejie567/R2DIO.git
    cd ..
    catkin_make
    source ~/catkin_ws/devel/setup.bash
```

### 3.2 Download test rosbag
You may download our [recorded data](https://drive.google.com/file/d/11LRsnL8Be4eK5r5jWjqNwo1AqkY_aUzp/view?usp=sharing) (10GB). (one rosbag)

If you are in China, you can download the recorded data via Baidu Netdisk
: [office](https://pan.baidu.com/s/1LTos6MG4CUq3SJz6GV55tQ), [hall](https://pan.baidu.com/s/16hp1APONPAn46WgFgvkm_g), and [display board](https://pan.baidu.com/s/1Ys_a9dZR9E-d9ELlY6-wug). The extraction code is 0503. (ten rosbags)

Note that due to the limitation of Google drive capacity, we only upload one rosbag. 




### 3.3 Launch ROS
```
    roslaunch r2dio r2dio.launch
```
Note that change the path to your datasets.

## 4. Sensor Setup
If you have new Realsense L515 sensor, you may follow the below setup instructions

### 4.1 IMU calibration (optional)
You may read official document [L515 Calibration Manual] (https://github.com/l515_calibration_manual.pdf) first

use the following command to calibrate imu, note that the build-in imu is a low-grade imu, to get better accurate, you may use your own imu
```
cd ~/catkin_ws/src/r2dio/l515_imu_calibration
python rs-imu-calibration.py
```

### 4.2 L515
<p align='center'>
<img width="35%" src="/img/realsense_L515.jpg"/>
</p>

### 4.3 Librealsense
Follow [Librealsense Installation](https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md)

### 4.4 Realsense_ros
Copy [realsense_ros](https://github.com/IntelRealSense/realsense-ros) package to your catkin folder
```
    cd ~/catkin_ws/src
    git clone https://github.com/IntelRealSense/realsense-ros.git
    cd ..
    catkin_make
```

### 4.5 Launch ROS
Make Lidar still for 1 sec to estimate the initial bias, otherwise will cause localization failure!
```
    roslaunch r2dio r2dio_L515.launch
```

## 5. Citation
If you use this work for your research, you may want to cite the paper below, your citation will be appreciated 
```
@article{wang2021lightweight,
  author={H. {Wang} and C. {Wang} and L. {Xie}},
  journal={IEEE Robotics and Automation Letters}, 
  title={Lightweight 3-D Localization and Mapping for Solid-State LiDAR}, 
  year={2021},
  volume={6},
  number={2},
  pages={1801-1807},
  doi={10.1109/LRA.2021.3060392}}
```
