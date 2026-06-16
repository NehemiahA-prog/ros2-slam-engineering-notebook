# Phase 02 — Learning Log

## Date Started

June 2026

## Main Goal

Understand how robots describe position and orientation mathematically and how ROS2 uses coordinate frames to represent the robot, the environment, and sensor data.

## What I Studied

- Position
- Orientation
- Pose
- Cartesian coordinate systems
- Robot frame / `base_link`
- Map frame / `map`
- Odometry frame / `odom`
- Coordinate transforms
- ROS2 TF tree structure
- Why `map`, `odom`, and `base_link` are separate

## Key Concepts Learned

### Position

Position describes where the robot is inside a coordinate frame.

Example:

```text
(4, 2)
```

This gives location, but not direction.

### Orientation

Orientation describes which way the robot is facing.

Example:

```text
90 degrees
```

This can mean the robot is facing positive Y in a standard map coordinate system.

### Pose

Pose combines position and orientation.

Example:

```text
(4, 2, 90 degrees)
```

This describes both where the robot is and which way it is facing.

## Frame Takeaways

### base_link

The robot's own coordinate frame.

The robot is always at `(0, 0)` in its own frame.

This frame answers:

```text
Where are things relative to me?
```

### odom

The odometry frame.

It is smooth and continuous, but it drifts over time.

This frame answers:

```text
Based on my sensors, where do I think I am?
```

### map

The globally corrected map frame.

It is corrected by localization or SLAM.

This frame answers:

```text
Where am I after SLAM corrections?
```

## Important Understanding

A robot at the same position can behave differently depending on orientation.

For example, if two robots are both at `(4, 2)` but one faces `0 degrees` and the other faces `90 degrees`, the command `move forward` will send them in different directions.

This is why pose is more complete than position alone.

## ROS2 TF Tree

A typical ROS2 frame relationship is:

```text
map
 ↓
odom
 ↓
base_link
 ↓
laser
```

TF allows ROS2 to convert coordinates between frames automatically.

## What Finally Clicked

The robot is always at the center of its own frame, but that does not mean the robot is at the center of the map.

In `base_link`, the robot is always at `(0, 0)` because the frame moves with the robot.

In `map`, the robot may be at `(4, 2)` or somewhere else because the map frame is attached to the world.

In `odom`, the robot is where its motion sensors estimate it to be, but that estimate can drift.

SLAM helps correct that drift by updating the relationship between `map` and `odom`.

## Simple Explanation

Pose means:

```text
Where the robot is and which way it is facing.
```

Just like finding a friend in a cafeteria requires knowing both where they are standing and which direction they are facing, a robot needs both position and orientation to understand its location.

## Next Steps

- Study odometry in more detail.
- Understand how encoder data creates movement estimates.
- Learn how drift happens.
- Connect pose and coordinate frames to Phase 03 odometry.
