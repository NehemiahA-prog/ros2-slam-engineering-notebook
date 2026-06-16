# Phase 02 — Answers

## Goal

Understand how robots describe position and orientation mathematically and how ROS2 uses coordinate frames to represent the robot, the environment, and sensor data.

---

## 1. What is position?

Position is the location of an object within a coordinate system.

Position answers the question:

**Where is the robot?**

Example:

```text
(4, 2)
```

This means the robot is located at:

- `x = 4`
- `y = 2`

relative to some coordinate frame.

Position alone does not describe which direction the robot is facing.

---

## 2. What is orientation?

Orientation describes the direction the robot is facing.

Orientation answers the question:

**Which way is the robot pointing?**

In robotics, orientation is commonly represented using theta or degrees.

Example:

```text
90 degrees
```

This indicates the robot is facing the positive Y direction in a standard map coordinate system.

Two robots can have the same position but different orientations.

---

## 3. What is pose?

Pose is the combination of a robot's position and orientation.

Pose answers the question:

**Where is the robot and which direction is it facing?**

Example:

```text
(4, 2, 90 degrees)
```

where:

- `4` = x position
- `2` = y position
- `90 degrees` = orientation

Pose is the complete mathematical description of the robot's location.

---

## 4. What coordinate system does the robot use?

Robots commonly use a Cartesian coordinate system.

```text
       +Y
        ↑
        |
        |
--------+--------→ +X
        |
        |
```

The origin is:

```text
(0, 0)
```

All positions are measured relative to a coordinate frame.

Coordinates are meaningless unless the frame is specified.

---

## 5. What is the robot frame?

The robot frame is the coordinate system attached directly to the robot.

In ROS2, this frame is typically called:

```text
base_link
```

The robot frame moves with the robot.

The robot is always located at:

```text
(0, 0)
```

within its own frame.

The robot frame answers:

**Where are objects relative to me?**

Example:

```text
Chair = (1, 0)
```

This means the chair is 1 meter in front of the robot.

---

## 6. What is the map frame?

The map frame is a fixed coordinate system attached to the environment.

In ROS2, this frame is called:

```text
map
```

The map frame does not move.

The map frame answers:

**Where is the robot within the world?**

SLAM continuously updates the robot's position within the map frame.

Example:

```text
Robot = (4, 2)
```

This means the robot is located at coordinate `(4, 2)` in the environment.

---

## 7. What is the odom frame?

The odom frame is the coordinate system generated from odometry.

In ROS2, this frame is called:

```text
odom
```

Odometry is calculated using:

- Wheel encoders
- IMU
- Sensor fusion such as an Extended Kalman Filter, or EKF

The odom frame provides a smooth estimate of the robot's motion.

The odom frame answers:

**Based on my motion sensors, where do I think I am?**

The odom frame gradually accumulates error and drift over time.

---

## 8. Why do coordinate transforms exist?

Different coordinate frames describe the same object from different perspectives.

Example:

Robot frame:

```text
Chair = (1, 0)
```

Map frame:

```text
Chair = (5, 3)
```

Both descriptions are correct.

A transform is the mathematical relationship between two coordinate frames.

Transforms allow ROS2 to convert information between frames.

Transforms answer the question:

**How do I describe the same object in another coordinate system?**

---

## Understanding

## 9. If the robot rotates 90 degrees, what changes?

Position:

```text
Does not change
```

Orientation:

```text
Changes
```

Pose:

```text
Changes
```

Example before rotation:

```text
(4, 2, 0 degrees)
```

Example after rotation:

```text
(4, 2, 90 degrees)
```

The robot remains in the same location but faces a different direction.

---

## 10. If the robot moves forward 1 meter, what changes?

Position:

```text
Changes
```

Orientation:

```text
Does not change
```

Pose:

```text
Changes
```

Example before movement:

```text
(4, 2, 90 degrees)
```

Example after movement:

```text
(4, 3, 90 degrees)
```

The robot moves but continues facing the same direction.

---

## 11. How can the robot describe its location mathematically?

The robot describes its location using its pose.

Pose is represented as:

```text
(x, y, theta)
```

Example:

```text
(4, 2, 90 degrees)
```

This provides:

- Position
- Orientation

Together, position and orientation fully describe the robot's location.

---

## Additional Concepts Learned

## Why orientation matters

Position alone is insufficient for navigation.

Example:

Two robots may share the same position:

```text
(4, 2)
```

but have different orientations:

```text
0 degrees
90 degrees
180 degrees
270 degrees
```

A command such as:

```text
Move forward
```

produces a different result depending on orientation.

Orientation determines how movement commands affect future position.

---

## Why multiple frames exist

Different frames answer different questions.

### base_link

Answers:

**Where are things relative to me?**

### odom

Answers:

**Based on my sensors, where do I think I am?**

### map

Answers:

**After SLAM corrections, where am I actually?**

No single frame can answer all three questions effectively.

---

## Why odom and map are separate

The odom frame is:

- Fast
- Smooth
- Continuous

but accumulates drift.

The map frame is:

- Corrected by SLAM
- Globally accurate

but may occasionally adjust when corrections occur.

Separating these frames allows robots to maintain smooth motion estimates while correcting accumulated error.

---

## ROS2 TF Tree

ROS2 represents frame relationships using TF.

A typical ROS2 navigation system uses:

```text
map
 ↓
odom
 ↓
base_link
 ↓
laser
```

### map

Globally corrected position.

### odom

Motion estimate.

### base_link

Robot frame.

### laser

LiDAR frame attached to the robot.

TF allows ROS2 to convert coordinates between frames automatically.

---

## Simpleton Test

## 12. Explain pose to a 10-year-old.

Imagine your friend is standing in the cafeteria.

To find them, you need to know:

1. Where they are standing.
2. Which direction they are facing.

Knowing both pieces of information is called their pose.

A robot's pose is simply where it is and which way it is facing.

---

## Key Takeaways

Position answers:

**Where am I?**

Orientation answers:

**Which way am I facing?**

Pose answers:

**Where am I and which way am I facing?**

`base_link` answers:

**Where are things relative to me?**

`odom` answers:

**Where do my sensors think I am?**

`map` answers:

**Where am I after SLAM corrections?**

TF answers:

**How do I convert information between frames?**

These concepts form the foundation for localization, navigation, odometry, and SLAM.
