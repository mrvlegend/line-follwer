🤖 Line Follower Robot using Arduino

This project implements a Line Follower Robot using Arduino, motor drivers, and IR sensors. The robot detects a line and moves accordingly by controlling two DC motors.

🚀 Features
Follows a line using 2 sensors (left & right)
Automatic direction correction (left/right turns)
Simple logic-based movement
Serial monitoring for debugging
🧠 How It Works

The robot uses two sensors:

Left Sensor (A0)

Right Sensor (A1)

Each sensor detects whether it is on the line or not based on a threshold value.

| Left Sensor | Right Sensor | Action       |
| ----------- | ------------ | ------------ |
| ON          | ON           | Move Forward |
| OFF         | ON           | Turn Right   |
| ON          | OFF          | Turn Left    |
| OFF         | OFF          | Stop         |

⚙️ Components Required
Arduino Uno (or compatible)
Motor Driver (L298N / L293D)
2 DC Motors
2 IR Sensors
Robot Chassis
Power Supply (Battery)
Jumper Wires
#🔌Pin Configuration
| Motor            | Arduino Pin |
| ---------------- | ----------- |
| Motor A Forward  | 2           |
| Motor A Backward | 3           |
| Motor B Forward  | 4           |
| Motor B Backward | 5           |
#Sensor Pins
| Sensor       | Arduino Pin |
| ------------ | ----------- |
| Left Sensor  | A0          |
| Right Sensor | A1          |

#🛠️ Code Overview
Reads sensor values using analogRead()
Compares values with a threshold
Controls motors using digitalWrite()
Uses functions for movement:
forward()
turnLeft()
turnRight()
stop()
📟 Debugging

The sensor values are printed to the Serial Monitor:

Serial.print("Left Sensor: ");
Serial.print(leftValue);
Serial.print(" Right Sensor: ");
Serial.println(rightValue);

Use this to adjust the threshold value.

⚡ Threshold Adjustment
const int threshold = 500;
Increase if sensors are too sensitive
Decrease if line is not detected properly
▶️ How to Run
Connect all components as per pin configuration
Upload the code to Arduino
Open Serial Monitor (9600 baud)
Place robot on the track
Power ON and observe movement
🔧 Future Improvements
Add PID control for smoother movement
Add speed control using PWM
Use more sensors for better accuracy
Add obstacle detection
⚠️ Notes
Ensure proper motor driver connections
Calibrate sensors before use
Use stable power supply
