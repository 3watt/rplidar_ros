# RPLIDAR ROS package


RPLIDAR 구동을 위한 패키지 - 우리가 사용한 모델은 [A2M8](http://vctec.co.kr/product/360%EB%8F%84-%EB%A0%88%EC%9D%B4%EC%A0%80-%EC%8A%A4%EC%BA%90%EB%84%88-%ED%82%A4%ED%8A%B8-2-rplidar-a2-360-degree-laser-scanner-development-kit-/9432/)과 [A3](https://www.slamtec.com/en/Lidar/A3) 모델이다

> A2M8은 `rplidar.launch`로 실행시키고, A3는 `rplidar_a3.launch`로 실행시킨다.

![스펙비교](https://github.com/3watt/rplidar_ros/blob/master/imags/specs.jpg)

ROS node and test application for RPLIDAR

Visit following Website for more details about RPLIDAR:

[rplidar roswiki](http://wiki.ros.org/rplidar)

[rplidar HomePage](http://www.slamtec.com/en/Lidar)

[rplidar SDK](https://github.com/Slamtec/rplidar_sdk)

[rplidar Tutorial](https://github.com/robopeak/rplidar_ros/wiki)


## How to run rplidar ros package


I. Run rplidar node and view in the rviz
------------------------------------------------------------
```bash
roslaunch rplidar_ros view_rplidar.launch (for RPLIDAR A1/A2)

roslaunch rplidar_ros view_rplidar_a3.launch (for RPLIDAR A3)

roslaunch rplidar_ros view_rplidar_s1.launch (for RPLIDAR S1)
```
You should see rplidar's scan result in the rviz.

**Notice: the different is serial_baudrate between A1/A2 and A3/S1**
>A1/A2 : 115200  
>A3/S1 : 256000

## RPLidar frame
---
RPLidar frame must be broadcasted according to picture shown in 


![A1 frame](https://github.com/3watt/rplidar_ros/blob/master/imags/rplidar_A1.png)
![A2 fram](https://github.com/3watt/rplidar_ros/blob/master/imags/rplidar_A2.png)

## Customizing

기존에 없던 최소거리 설정 기능이 추가되었음

### rplidar_a3.launch

```xml
<launch>
    <arg name="min_distance" default="0.30"/> #30cm 이내의 포인트들은 무시된다.
    <arg name="max_distance" default="20.0"/> #최대 관측 거리 20m
    <arg name="serial_baudrate" default="256000"/> #baudrate 설정, 상단에 모델에 적합한 값이 적혀 있음

    <node name="rplidarNode" pkg="rplidar_ros" type="rplidarNode" output="screen">
        <param name="serial_port" type="string" value="/dev/ttyUSB0"/> #포트 번호 맞춰주기
        <param name="serial_baudrate" type="int" value="$(arg serial_baudrate)"/>
        <param name="frame_id" type="string" value="laser"/>
        <param name="inverted" type="bool" value="false"/>
        <param name="angle_compensate" type="bool" value="true"/>
        <param name="min_distance" value="$(arg min_distance)"/>
        <param name="max_distance" value="$(arg max_distance)"/>
    </node>
</launch>
```
