# Original firmware pin map and hardware issues

This table is transcribed from `firmware/line_follower_original.cpp`. It is a **source-derived draft**, not a verified wiring diagram.

| Function | Original firmware pin(s) | Note |
|---|---|---|
| L298N motor enable | ENA D10, ENB D11 | **D10 PWM conflicts with Servo on Uno R3** |
| L298N motor direction | IN1 D5, IN2 D6, IN3 D7, IN4 D8 | Verify actual wiring |
| IR tracking | Left D3, right D4 | Logic assumes `LOW` indicates detected line |
| HC-SR04 | TRIG D13, ECHO D12 | Check voltage and timeout behavior |
| Servo | D9 | Servo library uses Timer1 on Uno |
| TCS3200 | S0 A0, S1 A1, S2 A2, S3 A3, OUT A4, LED A5 | Occupies Uno analog pins as digital GPIO |
| Battery sensing | A6 | **Unavailable on standard Uno R3**; never connect battery directly without a safe divider |

## Required verification

- Confirm exact MCU board revision, voltage rails, and final physical wiring.
- Assign motor PWM to timer-compatible pins without Servo interference.
- Redesign or remove A6 battery sensing for standard Uno R3 and calibrate the voltage divider.
- Confirm motor direction / wheel orientation in the real hardware.
- Calibrate ultrasonic and color sensing thresholds experimentally.
- Run a clean Arduino build and motor/obstacle/line-track tests before replacing the reference firmware with a validated `.ino`.

The original code's `BATTERY_PIN` and PWM issues are intentionally left visible in the reference snapshot; silently changing pins without knowing the actual hardware connections could create incorrect wiring instructions.
