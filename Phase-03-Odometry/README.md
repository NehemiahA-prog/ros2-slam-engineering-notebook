# Phase 03 — Odometry

## Goal

Understand how robots estimate movement, why those estimates drift over time, and why external correction methods such as localization and SLAM are necessary.

## Why This Phase Matters

Odometry is one of the first ways a mobile robot estimates motion. It allows the robot to estimate how far it has moved and how much it has turned using sensors such as wheel encoders and an IMU.

Odometry is fast and useful, but it is not perfect. Small motion errors accumulate over time and cause drift. Understanding odometry drift is essential before studying mapping, localization, and SLAM.

## Core Ideas

- Odometry estimates robot movement over time.
- Wheel encoders measure wheel rotation, not true robot position.
- IMUs measure acceleration and rotational motion.
- Odometry is a form of dead reckoning.
- Drift happens because small measurement errors accumulate.
- Wheel slip is a major source of odometry error.
- Calibration can reduce systematic error.
- Sensor fusion, such as an EKF, combines noisy sensor data into a better estimate.
- Localization and SLAM are needed to correct long-term odometry drift.

## MentorPi Frame Relationship

By the end of this phase, the primary coordinate frame relationship is:

```text
map
 ↓
odom
 ↓
base_link
```

| Frame | Meaning |
|---|---|
| `map` | Globally corrected frame from localization or SLAM. |
| `odom` | Smooth motion estimate from odometry. |
| `base_link` | Robot-centered frame attached to the MentorPi body. |

## Deliverables

- `Questions.md` — Phase 3 odometry questions.
- `Answers.md` — complete workbook answers.
- `Learning-Log.md` — key takeaways, reflections, and next steps.

## Completion Criteria

Phase 3 is complete when I can clearly explain:

- What odometry is
- How wheel encoders estimate movement
- Why wheel rotation is not the same as true robot movement
- Why odometry drifts over time
- Why odometry can work without GPS or LiDAR
- The difference between systematic and random error
- How calibration and sensor fusion improve estimates
- Why localization and SLAM are needed to correct odometry drift
