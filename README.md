# 🤖 PID Line Follower Robot using Arduino

A high-performance **PID-based Line Follower Robot** built using **Arduino Uno**, **5 IR Reflective Sensors**, and an **L298N Motor Driver**. Unlike traditional if-else (bang-bang) control, this robot uses a **Weighted Average Position Algorithm** and **PID Control** to achieve smooth, accurate, and stable line tracking.

---

## 🚀 Features

- ✅ PID-based line following
- ✅ 5 IR reflective sensor array
- ✅ Weighted average line position detection
- ✅ Smooth steering with differential motor speed control
- ✅ Adjustable PID gains (Kp, Ki, Kd)
- ✅ PWM motor speed control
- ✅ Serial Monitor debugging
- ✅ Easily tunable for different tracks

---

# 📷 Robot Overview

The robot continuously detects the line position using five IR sensors and calculates its deviation from the center. A PID controller then adjusts the speed of the left and right motors independently to keep the robot centered on the line.

---

# 🎯 Why PID for Line Following?

The primary objective of a line-following robot is to remain centered on a black line while moving at high speed.

Traditional **Bang-Bang Control (If-Else Logic)** causes:

- Sudden turns
- Oscillation
- Zig-zag movement
- Reduced speed

PID Control continuously adjusts motor speed according to how far the robot has deviated from the center, resulting in:

- Smooth movement
- Better stability
- Faster recovery
- Higher accuracy
- Less oscillation

---

# 🧠 Working Principle

The robot reads values from five IR sensors arranged in a straight line.

```
       Front View

    [ S0 ][ S1 ][ S2 ][ S3 ][ S4 ]

         Robot Direction
               ↑
```

Sensor meanings

- **S0** → Far Left
- **S1** → Left
- **S2** → Center
- **S3** → Right
- **S4** → Far Right

Typical sensor output

- White Surface → High Value
- Black Line → Low Value

---

# ⚙️ Why Not Use Threshold Logic?

Binary logic works like this:

```
if(sensor > threshold)
    White
else
    Black
```

Although simple, this approach cannot determine:

- How far the robot is from the line
- Whether the deviation is small or large

It only knows:

```
Line Detected
or
No Line
```

This results in jerky robot movement.

---

# 📐 Weighted Average Position Calculation

Instead of binary detection, every sensor contributes to finding the exact position of the line.

Each sensor has a weight.

| Sensor | Weight |
|---------|-------:|
| S0 | -2 |
| S1 | -1 |
| S2 | 0 |
| S3 | +1 |
| S4 | +2 |

The line position is calculated using:

```text
Position =
Σ (Sensor Value × Weight)
-------------------------
Σ Sensor Values
```

Examples

### Line at Center

```
S0  S1  S2  S3  S4

0   0   1   0   0

Position = 0
```

---

### Line Slightly Left

```
1   1   0   0   0

Position = -1.5
```

Robot turns left.

---

### Line Slightly Right

```
0   0   0   1   1

Position = +1.5
```

Robot turns right.

---

# 🎯 Error Calculation

Desired Position

```text
Setpoint = 0
```

Robot Error

```text
Error = Setpoint − Position
```

Meaning

| Error | Robot Position | Action |
|--------|----------------|--------|
| 0 | Center | Move Straight |
| Positive | Line Left | Turn Left |
| Negative | Line Right | Turn Right |

---

# 🧮 PID Controller

The PID controller minimizes the tracking error using three components.

### Proportional (P)

Responds to the current error.

```text
P = Kp × Error
```

---

### Integral (I)

Accumulates previous errors.

```text
I = I + Error
```

Helps eliminate steady-state error.

---

### Derivative (D)

Predicts future error.

```text
D = Error − Previous Error
```

Helps reduce overshoot.

---

### Complete PID Equation

```text
PID =
(Kp × Error)
+
(Ki × Integral)
+
(Kd × Derivative)
```

---

# 🚗 Motor Speed Control

The PID output is used to modify motor speeds.

```text
Left Motor Speed  = Base Speed − PID

Right Motor Speed = Base Speed + PID
```

Example

```
Base Speed = 150

PID = 20

Left Motor  = 130

Right Motor = 170
```

Robot smoothly turns right.

---

# ⚙️ Components Required

- Arduino Uno
- L298N Motor Driver
- 5 IR Reflective Sensors
- Two DC Geared Motors
- Robot Chassis
- Wheels
- Battery Pack
- Jumper Wires

---

# 🔌 Pin Configuration

## Motor Driver

| Function | Arduino Pin |
|-----------|-------------|
| Left Motor IN1 | 2 |
| Left Motor IN2 | 3 |
| Right Motor IN1 | 4 |
| Right Motor IN2 | 5 |
| Left PWM | 9 |
| Right PWM | 10 |

---

## Sensor Connections

| Sensor | Arduino Pin |
|---------|-------------|
| S0 | A0 |
| S1 | A1 |
| S2 | A2 |
| S3 | A3 |
| S4 | A4 |

---

# 💻 Code Workflow

1. Read all sensor values.
2. Normalize sensor readings.
3. Calculate weighted average position.
4. Compute error.
5. Calculate PID output.
6. Adjust motor speeds.
7. Repeat continuously.

---

# 📟 Serial Debugging

Useful values displayed on Serial Monitor:

```cpp
Sensor Values

Line Position

Error

PID Output

Left Motor Speed

Right Motor Speed
```

---

# 🎛 PID Tuning

The robot performance depends on selecting proper PID constants.

### Increase Kp

- Faster correction
- More oscillation

### Increase Ki

- Removes steady-state error
- Too much causes instability

### Increase Kd

- Smoother movement
- Reduces overshoot

Typical starting values

```cpp
Kp = 18

Ki = 0

Kd = 12
```

Tune according to your robot.

---

# ▶️ How to Run

1. Assemble the robot.
2. Connect all sensors.
3. Upload the Arduino sketch.
4. Open Serial Monitor.
5. Place the robot on the track.
6. Tune Kp, Ki, and Kd if necessary.
7. Observe smooth PID-based line following.

---

# 📈 Advantages of PID Line Following

- Smooth navigation
- High-speed operation
- Reduced oscillation
- Accurate line tracking
- Better corner handling
- Improved stability
- Faster recovery after deviation

---

# 🔧 Future Improvements

- Auto PID tuning
- Adaptive speed control
- Intersection detection
- Maze solving
- Bluetooth tuning interface
- OLED display for live PID values
- Encoders for precise odometry

---

# 📚 Technologies Used

- Arduino IDE
- Embedded C
- PID Control
- Weighted Average Algorithm
- PWM Motor Control
- Robotics
- Sensor Interfacing

---

# 👨‍💻 Author

**Vijeth B K**

Electronics & Communication Engineer

Embedded Systems • Robotics • STM32 • Arduino • Raspberry Pi • IoT

---
