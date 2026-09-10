````markdown
#  Hand Gesture Control Car

A wireless robotic car controlled using **hand gestures**.

This project uses an **MPU6050 accelerometer and gyroscope**, **Arduino**, and **HC-05 Bluetooth modules** to create a wireless gesture-controlled robotic car.

The system is divided into two main parts:

- **Transmitter** — detects the user's hand orientation and generates movement commands.
- **Receiver** — receives the commands wirelessly and controls the robotic car motors.

The user can control the car by changing the orientation of their hand instead of using a conventional joystick or remote controller.

---

#  Project Overview

The Hand Gesture Control Car is an embedded robotics project that demonstrates **gesture-based human-machine interaction**.

The transmitter consists of an Arduino, MPU6050 motion sensor, and HC-05 Bluetooth module.

The MPU6050 detects the orientation and movement of the user's hand. The transmitter Arduino processes this information and determines the required movement command.

The command is then transmitted wirelessly through Bluetooth to another HC-05 module connected to the receiver Arduino.

The receiver Arduino interprets the received command and controls the motor driver, which drives the DC motors of the robotic car.

### Overall Flow

```text
Hand Gesture
     │
     ▼
  MPU6050
     │
     ▼
Transmitter Arduino
     │
     ▼
Movement Command
     │
     ▼
HC-05 Bluetooth
     │
     │ Wireless Communication
     ▼
HC-05 Bluetooth
     │
     ▼
Receiver Arduino
     │
     ▼
Motor Driver
     │
     ▼
DC Motors
     │
     ▼
Robotic Car
````

---

#  Features

* Hand gesture-based car control
* Wireless control
* MPU6050 accelerometer and gyroscope
* HC-05 Bluetooth communication
* Arduino-based transmitter
* Arduino-based receiver
* Real-time movement commands
* Forward movement
* Reverse movement
* Left movement
* Right movement
* Stop command
* No conventional joystick required
* Simple character-based command communication
* Separate transmitter and receiver systems
* Circuit diagrams included
* Demonstration photos included
* Demonstration videos included
* Modular embedded-system architecture

---

#  Working Principle

The project is divided into four major stages:

1. Gesture Detection
2. Command Generation
3. Wireless Transmission
4. Motor Control

---

## 1. Gesture Detection

The **MPU6050** is connected to the transmitter Arduino.

The MPU6050 contains:

* Accelerometer
* Gyroscope
* Digital Motion Processor (DMP)

The sensor provides motion and orientation information through the **I2C interface**.

The transmitter processes the sensor data and uses the orientation information to determine the intended movement of the car.

The MPU6050 DMP functionality is used by the transmitter program for motion/orientation processing.

---

## 2. Command Generation

After determining the hand orientation, the transmitter generates a simple character-based movement command.

| Command | Intended Action |
| ------- | --------------- |
| `F`     | Forward         |
| `B`     | Reverse         |
| `L`     | Left            |
| `R`     | Right           |
| `S`     | Stop            |

These commands are then sent to the Bluetooth module.

Using single-character commands keeps the communication simple and lightweight.

---

## 3. Wireless Transmission

The transmitter Arduino sends the movement command through an **HC-05 Bluetooth module**.

A second HC-05 Bluetooth module is connected to the receiver Arduino on the robotic car.

The receiver Bluetooth module receives the command and passes it to the receiver Arduino.

```text
Transmitter Arduino
        │
        │ Movement Command
        ▼
   HC-05 Module
        │
        │ Bluetooth
        ▼
   HC-05 Module
        │
        ▼
Receiver Arduino
```

---

## 4. Motor Control

The receiver Arduino reads the incoming Bluetooth command.

Depending on the received command, the receiver activates the corresponding motor-control outputs.

The motor driver receives these control signals and controls the DC motors.

The motors then produce the required movement of the robotic car.

```text
Bluetooth Command
        │
        ▼
Receiver Arduino
        │
        ▼
Motor Driver
        │
        ▼
DC Motors
        │
        ▼
Car Movement
```

---

#  System Architecture

```text
                    USER
                     │
                     │ Hand Movement
                     ▼
              ┌──────────────┐
              │    MPU6050   │
              └──────┬───────┘
                     │
                     │ I2C
                     ▼
              ┌──────────────┐
              │  Transmitter │
              │    Arduino   │
              └──────┬───────┘
                     │
                     │ Serial
                     ▼
              ┌──────────────┐
              │     HC-05    │
              │  Transmitter │
              └──────┬───────┘
                     │
                     │
             Wireless Bluetooth
                     │
                     │
              ┌──────▼───────┐
              │     HC-05    │
              │   Receiver   │
              └──────┬───────┘
                     │
                     │ Serial
                     ▼
              ┌──────────────┐
              │   Receiver   │
              │    Arduino   │
              └──────┬───────┘
                     │
                     ▼
              ┌──────────────┐
              │ Motor Driver │
              └──────┬───────┘
                     │
                     ▼
              ┌──────────────┐
              │   DC Motors  │
              └──────┬───────┘
                     │
                     ▼
                 CAR MOTION
```

---

#  Hardware Requirements

## Transmitter

* Arduino board
* MPU6050 accelerometer and gyroscope module
* HC-05 Bluetooth module
* Connecting wires
* Suitable power source
* Hand-held or wearable mounting arrangement

## Receiver / Car

* Arduino board
* HC-05 Bluetooth module
* Motor driver
* DC geared motors
* Robotic car chassis
* Wheels
* Battery / power source
* Connecting wires

---

#  Software Requirements

* Arduino IDE
* Arduino / C++
* MPU6050 library
* I2Cdev library
* Wire library
* SoftwareSerial library

The MPU6050 and I2Cdev source files required by the project are included inside the repository.

---

#  Libraries

The project contains the required MPU6050 and I2Cdev library files inside:

```text
codes/Libraries/
```

The included files are:

```text
helper_3dmath.h
I2Cdev.cpp
I2Cdev.h
MPU6050.cpp
MPU6050.h
MPU6050_6Axis_MotionApps20.h
```

The Arduino code also uses:

```cpp
Wire
SoftwareSerial
```

The required library source files are included in the repository so that the project contains the necessary MPU6050/I2Cdev components alongside the Arduino sketches.

---

#  Bluetooth Communication

The project uses **HC-05 Bluetooth modules** for wireless communication between the hand-held transmitter and the robotic car.

The transmitter sends movement commands as single characters.

```text
F → Forward
B → Reverse
L → Left
R → Right
S → Stop
```

The receiver reads the received character and performs the corresponding motor-control operation.

### Communication Process

```text
Gesture
   ↓
MPU6050
   ↓
Transmitter Arduino
   ↓
Character Command
   ↓
HC-05
   ↓
Bluetooth
   ↓
HC-05
   ↓
Receiver Arduino
   ↓
Motor Driver
   ↓
Car
```

---

#  Gesture Control

The transmitter converts hand orientation into movement commands.

| Gesture / Orientation  | Command | Car Action |
| ---------------------- | ------- | ---------- |
| Forward gesture        | `F`     | Forward    |
| Backward gesture       | `B`     | Reverse    |
| Left gesture           | `L`     | Left       |
| Right gesture          | `R`     | Right      |
| Neutral / stop gesture | `S`     | Stop       |

The exact sensor thresholds and orientation-processing logic are implemented directly in:

```text
codes/transmitter[gesture]/transmitter.ino
```

---

#  Transmitter Connections

The transmitter uses the MPU6050 through the Arduino's **I2C interface**.

The Bluetooth module is connected using `SoftwareSerial`.

According to the transmitter source code:

| Arduino Pin | Function          |
| ----------- | ----------------- |
| D10         | SoftwareSerial RX |
| D11         | SoftwareSerial TX |

The MPU6050 communicates through the Arduino's I2C interface.

The exact physical wiring should be followed using the transmitter circuit diagram included in the repository.

---

#  Receiver Connections

The receiver Arduino receives commands from the Bluetooth module and sends motor-control signals to the motor driver.

According to the receiver source code, the motor-control interface uses:

| Arduino Pin | Function      |
| ----------- | ------------- |
| D3          | Motor control |
| D5          | Motor control |
| D6          | Motor control |
| D9          | Motor control |

The exact motor-driver wiring should be followed according to the receiver circuit diagram.

---

#  Circuit Diagrams

Circuit diagrams for both the transmitter and receiver are included in the repository.

```text
circuit diagram/
├── circuit-diagram-transmitter
└── circuit-diagram-receiver
```

## Transmitter Circuit

The transmitter circuit contains the components required for:

* MPU6050 motion sensing
* Arduino processing
* HC-05 Bluetooth transmission

## Receiver Circuit

The receiver circuit contains the components required for:

* HC-05 Bluetooth reception
* Arduino command processing
* Motor-driver control
* DC motor operation

Refer to the provided circuit diagrams when assembling the hardware.

---

#  Project Structure

```text
Hand Gesture Control Car/
│
├── codes/
│   │
│   ├── Libraries/
│   │   ├── helper_3dmath.h
│   │   ├── I2Cdev.cpp
│   │   ├── I2Cdev.h
│   │   ├── MPU6050.cpp
│   │   ├── MPU6050.h
│   │   └── MPU6050_6Axis_MotionApps20.h
│   │
│   ├── transmitter[gesture]/
│   │   └── transmitter.ino
│   │
│   └── receiver[car]/
│       └── receiver.ino
│
├── demo/
│   ├── photos/
│   └── videos/
│
├── circuit diagram/
│   ├── circuit-diagram-transmitter
│   └── circuit-diagram-receiver
│
├── README.md
├── LICENSE
└── .gitignore
```

---

#  Installation & Setup

## 1. Install Arduino IDE

Install the Arduino IDE on your computer.

Connect the transmitter Arduino to the computer using USB.

---

## 2. Open the Transmitter Code

Navigate to:

```text
codes/transmitter[gesture]/transmitter.ino
```

Open the sketch in Arduino IDE.

---

## 3. Verify the Libraries

Make sure the MPU6050/I2Cdev files available in:

```text
codes/Libraries/
```

are accessible to the Arduino project.

---

## 4. Upload the Transmitter

Select the correct:

* Arduino board
* COM port

Then compile and upload:

```text
transmitter.ino
```

---

## 5. Upload the Receiver

Connect the receiver Arduino and open:

```text
codes/receiver[car]/receiver.ino
```

Select the appropriate Arduino board and COM port and upload the receiver program.

---

## 6. Configure Bluetooth

Configure the HC-05 modules so that the transmitter and receiver can communicate with each other.

The two Bluetooth modules must be correctly configured and paired before testing wireless control.

---

## 7. Assemble the Hardware

Connect the components according to:

```text
circuit diagram/circuit-diagram-transmitter
```

and:

```text
circuit diagram/circuit-diagram-receiver
```

---

## 8. Power the System

Provide the appropriate power supply to the transmitter and receiver/car.

Ensure that:

* Arduino boards receive suitable power.
* The MPU6050 is powered correctly.
* The Bluetooth modules are powered correctly.
* The motor driver receives the required motor supply.
* The battery can provide sufficient current for the motors.

---

## 9. Test the Car

After establishing Bluetooth communication:

1. Power the transmitter.
2. Power the robotic car.
3. Verify Bluetooth communication.
4. Keep the hand in the neutral position.
5. Test the forward gesture.
6. Test the reverse gesture.
7. Test the left gesture.
8. Test the right gesture.
9. Test the stop gesture.

---

#  Testing

The project should be tested one movement at a time.

### Basic Test Flow

```text
Power ON
   ↓
Initialize MPU6050
   ↓
Initialize Bluetooth
   ↓
Detect Hand Orientation
   ↓
Generate Command
   ↓
Transmit Command
   ↓
Receive Command
   ↓
Control Motor Driver
   ↓
Car Movement
```

### Movement Test

| Test             | Expected Command | Expected Result    |
| ---------------- | ---------------- | ------------------ |
| Forward gesture  | `F`              | Car moves forward  |
| Backward gesture | `B`              | Car moves backward |
| Left gesture     | `L`              | Car turns left     |
| Right gesture    | `R`              | Car turns right    |
| Stop gesture     | `S`              | Car stops          |

Testing should verify that every supported gesture produces the expected command and corresponding vehicle movement.

---

#  Demo

Demonstration material is included in the repository.

```text
demo/
├── photos/
└── videos/
```

---

## Demo Photos

Project photographs are available in:

```text
demo/photos/
```

Images can be displayed directly in this README.

Example:

```markdown
![Hand Gesture Control Car](demo/photos/example.jpg)
```

Replace `example.jpg` with the actual image filename.

---

## Demo Videos

Project demonstration videos are available in:

```text
demo/videos/
```

Large video files may be hosted separately and linked from this section if required.

---

#  Applications

The concept of gesture-based vehicle control can be used as a foundation for:

* Educational robotics
* Human-machine interaction
* Gesture-controlled robotic systems
* Remote-controlled vehicles
* Assistive robotics
* Embedded-system demonstrations
* Robotics laboratories
* IoT and embedded projects
* Experimental vehicle-control systems
* Human-controlled robotic platforms

---

#  Future Improvements

The current project can be extended in several ways.

## Gesture Recognition

* Add more gesture commands
* Improve gesture classification
* Add configurable gesture sensitivity
* Improve robustness against accidental movements
* Add gesture calibration

## Vehicle Control

* Add variable speed control
* Add acceleration and deceleration control
* Add an emergency-stop gesture
* Add additional vehicle functions
* Add smoother turning control

## Sensors

Additional sensors could be integrated for:

* Obstacle detection
* Distance measurement
* Collision avoidance
* Environmental sensing

## Communication

The wireless system could be extended with:

* Telemetry
* Battery status
* Sensor feedback
* Two-way communication
* Longer-range communication technologies

## Advanced Robotics

Future versions could integrate:

* Camera-based gesture recognition
* Computer vision
* Machine-learning-based gesture classification
* Autonomous navigation
* Obstacle avoidance
* Advanced robotic control

---

#  Limitations

* Gesture recognition depends on MPU6050 sensor readings.
* Sensor orientation and mounting affect gesture detection.
* Bluetooth communication has a limited effective range.
* The system depends on proper Bluetooth configuration.
* Motor performance depends on the motor driver, motors, battery, and chassis.
* Gesture thresholds are implemented in the transmitter code and may require adjustment for different physical setups.
* Sensor noise can affect gesture detection.
* The system is intended primarily as a gesture-controlled robotic vehicle rather than a fully autonomous vehicle.

---

#  Troubleshooting

## Car Does Not Respond to Gestures

Check:

* Bluetooth module power
* Bluetooth pairing/configuration
* Transmitter Arduino power
* Receiver Arduino power
* MPU6050 connections
* Motor-driver connections
* Battery connection
* Motor connections

---

## MPU6050 Is Not Responding

Check:

* I2C wiring
* Sensor power
* Ground connection
* SDA/SCL connections
* MPU6050 library availability
* Arduino board configuration

---

## Bluetooth Communication Is Not Working

Check:

* HC-05 power
* Serial connections
* SoftwareSerial pin connections
* Bluetooth configuration
* Transmitter/receiver pairing

The transmitter code uses:

```text
D10 → SoftwareSerial RX
D11 → SoftwareSerial TX
```

---

## Motors Are Not Moving

Check:

* Motor-driver power
* Motor connections
* Arduino control connections
* Battery voltage/current capability
* Receiver command processing
* Motor-driver wiring
* Circuit diagram

---

#  Technologies Used

| Technology     | Purpose                          |
| -------------- | -------------------------------- |
| Arduino        | Embedded control                 |
| C/C++          | Firmware development             |
| MPU6050        | Motion/orientation sensing       |
| I2C            | Sensor communication             |
| HC-05          | Wireless Bluetooth communication |
| SoftwareSerial | Serial communication             |
| DC Motors      | Vehicle movement                 |
| Motor Driver   | Motor control                    |

---

#  Project Architecture Summary

| Component           | Role                              |
| ------------------- | --------------------------------- |
| MPU6050             | Detects hand movement/orientation |
| Transmitter Arduino | Processes sensor data             |
| HC-05 Transmitter   | Sends movement commands           |
| HC-05 Receiver      | Receives movement commands        |
| Receiver Arduino    | Processes received commands       |
| Motor Driver        | Controls motor outputs            |
| DC Motors           | Move the robotic car              |

---

#  Design Approach

The project follows a simple modular architecture:

```text
SENSING
   ↓
PROCESSING
   ↓
COMMUNICATION
   ↓
COMMAND INTERPRETATION
   ↓
ACTUATION
```

Each major function is separated into a specific stage.

### Sensing

The MPU6050 captures the user's hand movement and orientation.

### Processing

The transmitter Arduino processes the sensor information and determines the appropriate movement command.

### Communication

The HC-05 Bluetooth modules provide wireless communication between the transmitter and receiver.

### Command Interpretation

The receiver Arduino interprets the received movement command.

### Actuation

The motor driver controls the DC motors to produce the required car movement.

---

#  Project Goals

The main goals of this project are:

* To explore gesture-based human-machine interaction.
* To interface an MPU6050 with an Arduino.
* To process motion and orientation information.
* To establish wireless communication using HC-05 Bluetooth.
* To control a robotic vehicle remotely.
* To demonstrate an alternative to conventional joystick-based control.
* To integrate sensing, communication, and motor control into one embedded system.
* To build a practical gesture-controlled robotic platform.

---

#  Learning Outcomes

This project provides practical experience with:

* Arduino programming
* Embedded C/C++
* Sensor interfacing
* MPU6050 motion sensing
* I2C communication
* Bluetooth communication
* Serial communication
* Motor-driver interfacing
* DC motor control
* Robotic vehicle design
* Hardware-software integration
* Human-machine interaction

---

#  Safety Considerations

When testing the robotic car:

* Keep the vehicle on a clear surface.
* Keep fingers away from moving wheels and motors.
* Ensure all wiring is properly insulated and secured.
* Use an appropriate battery and power source.
* Disconnect power before changing motor-driver wiring.
* Test the system at low speed where possible.
* Keep the car away from people, obstacles, and fragile objects during testing.

---

#  Contributing

Contributions, improvements, and suggestions are welcome.

To contribute:

1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Test the changes.
5. Commit your changes.
6. Push the branch.
7. Open a Pull Request.

---

#  License

This project is licensed under the **MIT License**.

See the `LICENSE` file for details.

---

#  Author

**Rohith Y B**

GitHub: **RohithYB-JR**

---

#  Acknowledgements

This project uses the **MPU6050** and **I2Cdev** libraries for interfacing with and processing data from the MPU6050 motion sensor.

---

#  Summary

The **Hand Gesture Control Car** demonstrates how motion sensing, embedded programming, wireless communication, and motor control can be combined to create a gesture-driven robotic vehicle.

The transmitter detects the user's hand orientation using an MPU6050, processes the sensor information using Arduino, converts the detected gesture into a movement command, and sends the command wirelessly through HC-05 Bluetooth.

The receiver receives the command through the second HC-05 module, processes it using Arduino, and controls the motor driver to move the robotic car.

```text
Hand Gesture
     ↓
MPU6050
     ↓
Transmitter Arduino
     ↓
Movement Command
     ↓
HC-05
     ↓
Wireless Bluetooth
     ↓
HC-05
     ↓
Receiver Arduino
     ↓
Motor Driver
     ↓
DC Motors
     ↓
Gesture-Controlled Car
```

---

