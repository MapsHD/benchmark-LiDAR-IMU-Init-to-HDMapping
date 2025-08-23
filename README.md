# lidar-imu-init-converter

## Intended use 

This small toolset allows to integrate SLAM solution provided by [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains ROS 1 workspace that :
  - submodule to tested revision of LiDAR_IMU_Init
  - a converter that listens to topics advertised from odometry node and save data in format compatible with HDMapping.

## Dependencies
```shell
sudo apt install -y nlohmann-json3-dev
sudo apt install libgflags-dev
sudo apt install libgoogle-glog-dev
```

## Ceres
```shell
cd ~
git clone https://ceres-solver.googlesource.com/ceres-solver
cd ceres-solver && git fetch --all --tags
git checkout tags/2.1.0
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

## Building

Clone the repo
```shell
mkdir -p /test_ws/src
cd /test_ws/src
git clone https://github.com/marcinmatecki/LiDAR-IMU-Init-to-HDMapping.git --recursive
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
roslaunch lidar_imu_init xxx.launch
rosbag play {path_to_bag}
```

## Usage - conversion:

```shell
cd /test_ws/
source ./install/setup.sh # adjust to used shell
rosrun lidar-imu-init-to-hdmapping listener <recorded_bag> <output_dir>
```
