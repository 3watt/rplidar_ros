RPLIDAR ROS package
=====================================================================

ROS node and test application for RPLIDAR

Visit following Website for more details about RPLIDAR:

rplidar roswiki: http://wiki.ros.org/rplidar

rplidar HomePage:   http://www.slamtec.com/en/Lidar

rplidar SDK: https://github.com/Slamtec/rplidar_sdk

rplidar Tutorial:  https://github.com/robopeak/rplidar_ros/wiki

How to build rplidar ros package
=====================================================================
    1) Clone this project to your catkin's workspace src folder
    2) Running catkin_make to build rplidarNode and rplidarNodeClient

How to run rplidar ros package
=====================================================================
There're two ways to run rplidar ros package

I. Run rplidar node and view in the rviz
------------------------------------------------------------
roslaunch rplidar_ros view_rplidar.launch (for RPLIDAR A1/A2)
,
roslaunch rplidar_ros view_rplidar_a3.launch (for RPLIDAR A3)
or
roslaunch rplidar_ros view_rplidar_s1.launch (for RPLIDAR S1)

You should see rplidar's scan result in the rviz.

II. Run rplidar node and view using test application
------------------------------------------------------------
roslaunch rplidar_ros rplidar.launch (for RPLIDAR A1/A2)
,
roslaunch rplidar_ros rplidar_a3.launch (for RPLIDAR A3)
or
roslaunch rplidar_ros rplidar_s1.launch (for RPLIDAR S1)

rosrun rplidar_ros rplidarNodeClient

You should see rplidar's scan result in the console

Notice: the different is serial_baudrate between A1/A2 and A3/S1

RPLidar frame
=====================================================================
RPLidar frame must be broadcasted according to picture shown in rplidar-frame.png

## Customizing

Kobuki에 RPLidar를 장착하기 위해서 다음과 같은 내용들을 수정하였음.

1. Kobuki USB와의 혼선을 방지하기 위해 Serial Port를 `/dev/ttyUSB0`에서 `/dev/ttyUSB1`로 설정해 두었음

`rplidar_ros -> launch -> rplidar.launch`

```xml
  <param name="serial_port"         type="string" value="/dev/ttyUSB1"/>
```

2. RPLidar가 Kobuki 바닥으로부터 10cm, Kobuki 정면 방향으로 부착된다는 가정 하에 `static_transform_publisher`를 설정해 두었음

```xml 
  <node pkg="tf" type="static_transform_publisher" name="laser" args="0 0 0.1 3.1415 0 0  base_scan laser 60"/>
```

3. RPLidar가 Kobuki 중앙에 부착된다는 가정 하에 Kobuki 금속 봉은 인식하지 않도록 `Mininum Range`를 `20cm`로 설정해 두었음

```c++
78    scan_msg.range_min = 0.2;
```
