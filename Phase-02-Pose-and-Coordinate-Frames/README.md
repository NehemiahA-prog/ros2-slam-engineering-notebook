# Phase 02 — Pose and Coordinate Frames

## Goal

Understand how robots describe position and orientation mathematically and how ROS2 uses coordinate frames to represent the robot, the environment, and sensor data.

## Why This Phase Matters

Robots need a precise way to describe where they are, which way they are facing, and how sensor data relates to the world around them.

Pose and coordinate frames are the foundation for odometry, localization, mapping, navigation, and SLAM. Without frames, sensor measurements and robot movement commands would not have clear meaning.

## Core Ideas

- **Position** describes where the robot is.
- **Orientation** describes which direction the robot is facing.
- **Pose** combines position and orientation.
- **base_link** describes the robot's own coordinate frame.
- **odom** describes the robot's smooth motion estimate from sensors.
- **map** describes the globally corrected frame used by SLAM.
- **TF** describes the mathematical relationships between coordinate frames.

## ROS2 Frame Relationship

A typical ROS2 navigation system uses a frame structure like this:

```text
map
 ↓
odom
 ↓
base_link
 ↓
laser
```

### Frame Meanings

| Frame | Meaning |
|---|---|
| `map` | Globally corrected position from localization or SLAM. |
| `odom` | Smooth motion estimate from odometry. |
| `base_link` | Robot frame attached to the robot body. |
| `laser` | LiDAR frame attached to the robot. |

## Deliverables

- `Questions.md` — Phase 2 questions.
- `Answers.md` — complete workbook answers.
- `Learning-Log.md` — key takeaways and next steps.

## Completion Criteria

Phase 2 is complete when I can clearly explain:

- Position, orientation, and pose
- The difference between robot frame, odom frame, and map frame
- Why coordinate transforms exist
- How ROS2 uses TF to connect coordinate frames
- Why odom and map are separate frames
- How pose supports localization, navigation, odometry, and SLAM
