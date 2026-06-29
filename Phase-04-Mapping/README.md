# Phase 04 — Mapping

## Goal

Understand how robots create mathematical representations of their environment using sensor data. Learn how LiDAR measurements become navigable maps and why mapping quality depends on both sensor accuracy and pose estimation.

## Why This Phase Matters

Mapping is the perception foundation for localization, navigation, and SLAM. A robot cannot navigate effectively unless it has a useful representation of free space, obstacles, and unknown areas.

For the MentorPi, mapping connects LiDAR measurements, robot pose, coordinate frames, and mapping algorithms into an occupancy grid that can be used for navigation.

## Core Ideas

- A robotic map is a mathematical representation of the environment.
- Robots use maps to represent free space, obstacles, and unexplored regions.
- Occupancy grids divide the environment into cells.
- Point clouds are created from many LiDAR measurements.
- LiDAR measures distance and angle, not object identity.
- Mapping algorithms combine LiDAR measurements with robot pose.
- Mapping quality depends on sensor accuracy, pose estimation, robot motion, and environmental structure.
- Poor odometry causes LiDAR points to be placed incorrectly, producing blurry or distorted maps.

## Mapping Pipeline

```text
Environment
 ↓
LiDAR
 ↓
Raw Distance Measurements
 ↓
Point Cloud
 ↓
Robot Pose (Odometry / Localization)
 ↓
Mapping Algorithm
 ↓
Occupancy Grid
 ↓
Navigation
```

The LiDAR does not create the map by itself. The mapping algorithm creates the map using LiDAR measurements and the robot's estimated pose.

## Deliverables

- `Questions.md` — Phase 4 mapping questions.
- `Answers.md` — complete workbook answers.
- `Learning-Log.md` — key takeaways, reflections, and next steps.

## Completion Criteria

Phase 4 is complete when I can clearly explain:

- What a robotic map is
- Why robots use occupancy grids instead of photographs
- How LiDAR creates distance measurements
- What point clouds are
- How LiDAR scans become maps
- Why map quality depends on pose estimation
- What causes bad maps
- Why feature-rich environments can be easier to map than featureless environments
- Why accurate mapping is required for localization, navigation, and SLAM
