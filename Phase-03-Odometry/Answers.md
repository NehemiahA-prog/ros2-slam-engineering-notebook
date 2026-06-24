# Phase 03 — Answers

## Goal

Understand how robots estimate movement, why those estimates drift over time, and why external correction methods such as localization and SLAM are necessary.

---

## 1. What is odometry?

Odometry is the process of estimating a robot's position and orientation by measuring its movement over time.

Rather than directly measuring its global location, the robot continuously estimates its pose using motion sensors such as wheel encoders and the IMU.

Odometry provides the robot's estimated pose in the `odom` coordinate frame.

### MentorPi Example

As the MentorPi drives, its wheel encoders measure wheel rotation while its IMU measures changes in acceleration and rotation.

Together, these sensors estimate how far the robot has moved and how much it has turned.

---

## 2. How do wheel encoders work?

Wheel encoders measure wheel rotation.

As each wheel rotates, the encoder counts the number of rotations or fractions of a rotation. Since the robot knows the wheel circumference, it can estimate the distance traveled.

Wheel encoders do not measure position directly. They only measure wheel rotation.

---

## 3. How does the robot estimate distance traveled?

The robot estimates distance by combining:

- Wheel circumference
- Number of wheel rotations

The basic idea is:

```text
Distance Traveled = Wheel Rotations × Wheel Circumference
```

For example, if a wheel circumference is `0.20 meters` and the encoder measures `10 complete rotations`, the robot estimates it has traveled approximately:

```text
10 × 0.20 = 2 meters
```

---

## 4. What causes odometry drift?

Odometry drift occurs because the robot assumes that wheel rotation perfectly represents robot movement.

In reality, several factors introduce errors, including:

- Wheel slip
- Uneven terrain
- Wheel wear
- Sensor noise
- Small measurement inaccuracies

These small errors accumulate over time, causing the robot's estimated position to gradually differ from its actual position.

---

## 5. Why is odometry never perfectly accurate?

Odometry is fundamentally an estimation process.

Although wheel encoders and IMUs provide valuable information, neither sensor directly measures the robot's true position within the environment.

Because every measurement contains some amount of error, these errors accumulate continuously as the robot moves.

For this reason, odometry alone can never provide perfect long-term localization.

---

## 6. Can odometry work without GPS?

Yes.

Odometry does not require GPS.

Instead, it estimates movement using wheel encoders and IMU measurements.

This is why indoor robots such as the MentorPi can still navigate and estimate movement even though GPS signals are unavailable.

GPS provides global position information, while odometry estimates movement relative to the robot's starting position.

---

## 7. Can odometry work without LiDAR?

Yes.

LiDAR is not required to perform odometry.

The robot can continue estimating movement using only wheel encoders and IMU data.

However, without LiDAR or another external reference, accumulated odometry drift cannot be corrected, causing localization errors to grow over time.

---

## 8. Why does wheel slip matter?

Wheel slip occurs when the wheels rotate without producing the expected amount of movement.

Odometry assumes:

```text
Wheel Rotation = Robot Movement
```

Wheel slip breaks this assumption.

As a result, the robot estimates motion that never actually occurred.

Wheel slip is one of the largest sources of odometry drift.

---

# Additional Concepts Learned

---

## Dead Reckoning

Odometry is a form of **dead reckoning**.

Dead reckoning estimates the robot's current position by starting from a known position and continuously adding each measured movement.

Rather than measuring its true location directly, the robot repeatedly estimates:

```text
Current Position = Previous Position + Estimated Movement
```

As errors accumulate, the estimated position gradually diverges from reality.

---

## Error Accumulation

Small errors may appear insignificant over short distances.

However, because odometry continuously integrates motion estimates, even tiny errors accumulate over time.

Example:

- `1 mm` error per meter
- After `2,000 meters`
- Approximately `2 meters` of accumulated position error

This accumulation of small errors is known as **odometry drift**.

---

## Systematic Error

Systematic errors are consistent, repeatable errors that occur in the same direction.

Examples include:

- Incorrect wheel diameter
- Encoder calibration errors
- Constant IMU bias
- Uneven wheel sizes

Because systematic errors are predictable, engineers often reduce them through calibration.

---

## Random Error

Random errors fluctuate unpredictably.

Examples include:

- Electrical noise
- Surface irregularities
- Small vibrations
- LiDAR measurement noise
- Camera sensor noise

Unlike systematic errors, random errors cannot be completely removed through calibration.

Instead, robotics systems reduce their effects using filtering and sensor fusion.

---

## Calibration

Calibration reduces systematic error by adjusting the robot's parameters to better match physical reality.

Examples include:

- Measuring actual wheel diameter
- Correcting encoder resolution
- Estimating IMU bias

Calibration improves odometry accuracy but cannot eliminate random noise.

---

## Sensor Fusion and the EKF

Every sensor contains uncertainty.

Wheel encoders, IMUs, LiDAR, GPS, and cameras all produce imperfect measurements.

Sensor fusion combines these measurements to produce a more reliable estimate of the robot's state.

The Extended Kalman Filter, or EKF, is one of the most common sensor fusion algorithms used in robotics.

Rather than trusting a single sensor, the EKF combines multiple noisy measurements to estimate the robot's most likely pose.

---

## Relationship Between Odometry, Localization, and SLAM

Odometry estimates the robot's motion.

Localization determines the robot's position within an existing map.

SLAM simultaneously builds a map while localizing the robot.

As odometry drift accumulates, localization and SLAM use external observations, such as LiDAR scans, to estimate a more accurate pose.

The corrected pose is represented in the `map` frame.

---

## MentorPi Coordinate Frames

By the end of Phase 3, the relationship between the primary coordinate frames is:

```text
map
 ↓
odom
 ↓
base_link
```

### base_link

The robot's coordinate frame.

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

Provides:

- Smooth motion
- Continuous updates

Limitation:

- Accumulates drift over time

### map

The global frame.

Answers:

```text
After localization or SLAM correction, where am I actually?
```

Provides:

- Globally corrected position
- Long-term localization accuracy

---

## Simpleton Test

## Explain odometry to a 10-year-old.

Imagine closing your eyes and counting every step you take.

You can guess where you are without looking.

That guessing process is called odometry.

The longer you walk without checking your surroundings, the more likely your guess becomes wrong.

---

## Key Takeaways

- Odometry estimates movement using wheel encoders and IMUs.
- Wheel encoders measure wheel rotation, not actual robot movement.
- Odometry is a form of dead reckoning.
- Small measurement errors accumulate over time, producing drift.
- Wheel slip is one of the largest causes of odometry error.
- GPS and LiDAR are not required for odometry, but external sensors are necessary to correct accumulated drift.
- Calibration reduces systematic error.
- Sensor fusion, such as an EKF, helps reduce the effects of random noise.
- Localization and SLAM provide corrected global pose estimates that compensate for odometry drift.

Phase 3 establishes the mathematical and conceptual foundation for Mapping, Localization, and SLAM.
