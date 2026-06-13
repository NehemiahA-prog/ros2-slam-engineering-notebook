# Phase 01 — Learning Log

## Date Started

June 2026

## Main Goal

Build foundational understanding of the MentorPi A1 robot, ROS2, localization, mapping, and SLAM before running physical experiments.

## What I Studied

- MentorPi A1 hardware overview
- Robot sensors used for navigation and perception
- ROS2 basic architecture
- Difference between localization, mapping, and SLAM
- How to explain robotics concepts simply

## Key Takeaways

- SLAM combines two hard problems: estimating position and building a map.
- LiDAR is important because it gives the robot distance measurements of the environment.
- Wheel encoders help estimate movement but can drift over time.
- ROS2 organizes robot software into nodes that communicate through topics and messages.
- A strong robotics engineer should be able to explain complex systems clearly.

## Questions I Still Have

- Where exactly does the MentorPi A1 expose IMU data in the ROS2 software stack?
- Where exactly does the MentorPi A1 expose wheel encoder or odometry data?
- Which ROS2 packages are used by the MentorPi A1 for SLAM and navigation?
- How does the robot combine LiDAR, odometry, and IMU data during navigation?

## Next Steps

- Locate MentorPi ROS2 topics for LiDAR, odometry, IMU, and camera data.
- Learn ROS2 coordinate frames and TF.
- Begin Phase 02 on pose and coordinate frames.
