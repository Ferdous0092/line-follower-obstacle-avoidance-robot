# Line-Following & Obstacle-Avoidance Robot

**University Engineering Project Portfolio · Soaib Ferdous**

This is my curated portfolio presentation of the line-following and obstacle-avoidance robot project I participated in during my university studies. The original project was developed collaboratively and was hosted through a different GitHub account.

- **Original repository:** https://github.com/alvi231078/D2---Line-Follower-Robot
- **Focus:** embedded robot control, sensor integration, real-time behavior models, system design, simulations, and mechanical integration
- **Repository status:** selected engineering artifacts; hardware/firmware reproduction is **not yet fully verified**

## What the robot does

The integrated source describes line tracking with two IR sensors, distance-based obstacle detection using an ultrasonic sensor, servo-assisted left/right scanning, differential motor control with an L298N driver, and optional color-based obstacle behavior. The algorithm uses timed movements and blocking delays rather than a complete non-blocking control scheduler.

## Engineering artifacts

| Folder | Content |
|---|---|
| `firmware/` | Original integrated Arduino C++ firmware snapshot; needs hardware pin review before use |
| `hardware/` | Source-derived pin map and unresolved wiring issues |
| `diagrams/` | Selected SysML architectural and behavioral diagrams |
| `models/uppaal/` | Line-following and obstacle timed-automata models |
| `models/simulink/` | Original IR-to-motor Simulink model (renamed `.slx` extension) |
| `electronics/` | Tinkercad schematic/evidence and LTspice circuit illustration |
| `mechanical/` | Updated vehicle assembly overview |
| `docs/` | Original technical report, kept unmodified |
| `CREDITS.md` | Portfolio context and source provenance |
| `RESTRICTED_LICENSE` | Original academic-use restrictions, unchanged |

## Firmware status: issues to resolve before claiming a reproducible build

The included `firmware/line_follower_original.cpp` is a **reference snapshot**, not validated final firmware for an Arduino Uno R3.

1. On a standard Arduino Uno R3, A6 is not available, yet the code uses `BATTERY_PIN = A6`.
2. The Servo library uses Timer1 on the Uno and interferes with PWM on pins 9 and 10; motor enable `ENA = 10` conflicts with this design.
3. The battery low-voltage conditional currently assigns `BASE_SPEED` in both branches, so it does not implement voltage-based speed control.
4. Timeout and failure handling around ultrasonic `pulseIn()` should be reviewed.
5. Source, report, and diagrams differ in some wiring details and thresholds. Use the verified hardware configuration as the final source of truth.

See [hardware/wiring.md](hardware/wiring.md) for the code-derived pin map.

## Verification and limitations

The repository includes models and design files, but should not be interpreted as a fresh validation of the full hardware system. The power-analysis data in the original repository was not selected for this curated package because its device assumptions are not fully aligned with the integrated Arduino Uno design. Experimental PID and other older prototype variants were also excluded rather than portrayed as integrated final features.

