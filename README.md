# lidar-map-init-converter

## Intended use 

This small toolset allows to integrate SLAM solution provided by [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains ROS 1 workspace that :
  - submodule to tested revision of LiDAR_IMU_Init
  - a converter that listens to topics advertised from odometry node and save data in format compatible with HDMapping.


## Building

Clone the repo
```shell
mkdir -p /test_ws/src
cd /test_ws/src
git clone https://github.com/marcinmatecki/Point-LIO-to-HDMapping.git --recursive
cd ..
catkin_make
```

## Usage - data SLAM:

Prepare recorded bag with estimated odometry:

In first terminal record bag:
```shell
rosbag record /cloud_registered /aft_mapped_to_init
```

and start odometry:
```shell 
cd /test_ws/
source ./install/setup.sh # adjust to used shell
roslaunch lidar_map_init xxx.launch
rosbag play {path_to_bag}
```

## Usage - conversion:

```shell
cd /test_ws/
source ./install/setup.sh # adjust to used shell
rosrun point-lio-to-hdmapping listener <recorded_bag> <output_dir>
```