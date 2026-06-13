# Phase 01 — Answers

## Robot Hardware

### 1. What sensors are on the MentorPi?

The MentorPi A1 documentation and kit materials commonly reference sensors used for robot perception and navigation, including LiDAR and a 3D depth camera. Depending on the exact kit configuration and software stack, the robot may also use an IMU and wheel encoder data for motion estimation.

### 2. What does each sensor measure?

- **LiDAR** measures distance to surrounding objects using laser scans.
- **3D depth camera** measures visual depth information and can help the robot understand objects and surfaces in front of it.
- **IMU** measures motion-related information such as acceleration and rotational movement.
- **Wheel encoders** measure wheel rotation, which can be used to estimate how far the robot has traveled.

### 3. Which sensor is most important for SLAM?

For 2D SLAM, LiDAR is usually one of the most important sensors because it provides distance measurements to surrounding walls, obstacles, and landmarks. These measurements help the robot build a map while estimating its position inside that map.

### 4. What information does the IMU provide?

An IMU provides information about the robot's movement and orientation changes. It typically measures acceleration and angular velocity. This helps estimate whether the robot is turning, tilting, speeding up, or slowing down.

### 5. What information do wheel encoders provide?

Wheel encoders provide information about how much the wheels rotate. This can be used to estimate distance traveled, speed, and changes in position. This estimate is called odometry.

### 6. Why does the robot need both LiDAR and encoders?

The robot needs both because each sensor helps with a different part of the problem. Encoders estimate how the robot moves over time, but that estimate can drift because of wheel slip or uneven surfaces. LiDAR observes the environment and can help correct that drift by comparing sensor readings to the map.

## ROS2

### 7. What is ROS2?

ROS2 is a robotics software framework that helps developers build robot systems out of smaller programs that communicate with each other.

### 8. Why do robotics companies use ROS2?

Robotics companies use ROS2 because it supports modular software design, communication between robot components, sensor integration, simulation, navigation, and reusable robotics tools.

### 9. What is a node?

A node is a small ROS2 program responsible for one part of the robot system. For example, one node may read LiDAR data, another may estimate odometry, and another may control movement.

### 10. What is a topic?

A topic is a named communication channel that ROS2 nodes use to send and receive data.

### 11. What is a message?

A message is the data structure sent over a ROS2 topic. For example, a LiDAR message may contain laser distance readings.

### 12. What is a launch file?

A launch file starts multiple ROS2 nodes together with the settings they need. This makes it easier to run a complete robot system.

## SLAM Overview

### 13. What does SLAM stand for?

SLAM stands for **Simultaneous Localization and Mapping**.

### 14. Why is SLAM considered difficult?

SLAM is difficult because the robot is trying to solve two problems at the same time. It must build a map of an unknown environment while also estimating where it is inside that map. Sensor noise, wheel slip, moving objects, and imperfect measurements make this harder.

### 15. What is the difference between localization and mapping?

Localization means estimating where the robot is. Mapping means building a representation of the environment. SLAM combines both problems when the robot does not already have a map.

## Simple Explanation Test

### 16. Explain localization to a 10-year-old.

Localization is how a robot figures out where it is, like looking around a room and realizing you are next to the door or beside the couch.

### 17. Explain mapping to a 10-year-old.

Mapping is how a robot draws a picture of the place it is exploring, like making a treasure map of a room or hallway.

### 18. Explain SLAM to a 10-year-old.

SLAM is when a robot explores a place it has never seen before, draws a map, and figures out where it is on that map at the same time.
