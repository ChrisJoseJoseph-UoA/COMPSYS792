**FAST-LIO2 Implementation Steps.**

Build the Docker container using the _Dockerfile_ available in ```/docker```. Then run the container by running ``` run_container.sh```.

To run, 

For every terminal, source the enviroment: 
```
source /opt/ros/noetic/setup.bash &&
source /root/livox_ws/devel/setup.bash &&
source /root/catkin_ws/devel/setup.bash
```

**Terminal A:**
```
roscore
```

**Terminal B:**
```   
roslaunch fast_lio mapping_mid360.launch
```

**Terminal C:**
```
rosrun pcl_ros pointcloud_to_pcd input:=/Laser_map _prefix:=/root/catkin_ws/src/FAST_LIO/PCD_Map/global_map_
```

**Terminal D:**
```
rosparam set use_sim_time true
rosbag play /root/rosbags/input/mid360/livoxmap.bag --clock
```

**For Large BAG files, use:**
```
roslaunch --sigint-timeout=480 --sigterm-timeout=480 fast_lio mapping_mid360.launch
rosnode kill /laserMapping
```
