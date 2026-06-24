# Phase 03 — Learning Log

## Date Completed

June 2026

## Main Goal

Understand how robots estimate movement, why those estimates drift over time, and why external correction methods such as localization and SLAM are necessary.

## What I Studied

- Odometry
- Wheel encoders
- IMU-based motion estimation
- Distance estimation from wheel rotations
- Odometry drift
- Wheel slip
- Dead reckoning
- Error accumulation
- Systematic error
- Random error
- Calibration
- Sensor fusion
- Extended Kalman Filter, or EKF
- Relationship between `map`, `odom`, and `base_link`

## Key Concepts Learned

### Odometry

Odometry estimates robot movement over time.

It does not directly measure the robot's true global position. Instead, it estimates pose based on measured movement.

For the MentorPi, this means using sensors such as wheel encoders and the IMU to estimate how far the robot has moved and how much it has turned.

### Wheel Encoders

Wheel encoders measure wheel rotation.

They do not directly measure robot position.

The robot estimates distance traveled using:

```text
Distance Traveled = Wheel Rotations × Wheel Circumference
```

This works well when the wheels roll cleanly, but it becomes inaccurate when the wheels slip or when the robot drives on uneven surfaces.

### Odometry Drift

Odometry drift happens because small motion estimation errors accumulate over time.

The robot may think it moved a certain distance or turned a certain amount, but the real movement may be slightly different.

Over time, these small differences become large enough to make the robot's estimated pose different from its actual pose.

## What Finally Clicked

Wheel encoders do not tell the robot where it is.

They only tell the robot how much the wheels rotated.

The robot then assumes that wheel rotation equals movement. That assumption is useful, but not always true.

This is why odometry is valuable but limited.

It gives the robot a smooth estimate of motion, but it cannot guarantee long-term accuracy.

## Error Types

### Systematic Error

Systematic error is consistent and repeatable.

Examples:

- Incorrect wheel diameter
- Encoder calibration error
- Constant IMU bias
- Uneven wheel sizes

These errors can often be reduced with calibration.

### Random Error

Random error changes unpredictably.

Examples:

- Electrical noise
- Small vibrations
- Surface irregularities
- Sensor noise

These errors cannot be completely removed, but filtering and sensor fusion can reduce their effect.

## Calibration Takeaway

Calibration improves the robot's estimate by making its software parameters better match the physical robot.

For example, if the software assumes the wheel diameter is slightly different from the real wheel diameter, every distance estimate will be slightly wrong.

Correcting that parameter reduces systematic odometry error.

## Sensor Fusion Takeaway

No single sensor is perfect.

Wheel encoders can be affected by slip.

IMUs can drift or contain bias.

LiDAR and cameras can contain measurement noise.

Sensor fusion combines multiple imperfect measurements to produce a better estimate than any single sensor alone.

The EKF is important because it estimates the robot's most likely state by combining noisy sensor inputs.

## Frame Understanding

By the end of Phase 3, the frame relationship is:

```text
map
 ↓
odom
 ↓
base_link
```

### base_link

The robot's own frame.

Answers:

```text
Where are objects relative to me?
```

### odom

The odometry frame.

Answers:

```text
Based on my motion sensors, where do I think I am?
```

It is smooth and continuous, but it drifts.

### map

The globally corrected frame.

Answers:

```text
After localization or SLAM correction, where am I actually?
```

It corrects accumulated drift using external observations.

## Simple Explanation

Odometry is like walking with your eyes closed and counting your steps.

At first, your guess about where you are might be close.

But the longer you walk without looking around, the more your estimate can become wrong.

Robots use odometry the same way. They estimate motion, but eventually they need external correction.

## Industry Relevance

Professional robotics systems use odometry constantly because robots need fast, smooth motion estimates.

However, industry systems rarely trust odometry alone for long-term navigation.

Autonomous robots typically combine odometry with sensors such as LiDAR, cameras, GPS, or depth sensors to correct drift.

This is important in robotics roles focused on:

- Localization
- SLAM
- Navigation
- Sensor fusion
- Autonomous systems

## Connection to Future Phases

Phase 3 explains why odometry alone is not enough.

That naturally leads into:

- **Phase 4 — Mapping:** how sensor data becomes a representation of the environment
- **Phase 5 — Localization:** how the robot corrects its pose inside a known map
- **Phase 6 — SLAM:** how the robot builds a map while estimating its corrected pose

## Final Takeaway

Odometry gives the robot a motion estimate, not the truth.

It is necessary because the robot needs continuous movement estimates, but it is limited because drift grows over time.

Localization and SLAM exist because robots need ways to correct odometry drift using observations of the environment.
