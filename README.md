A complete embedded-systems project implementing an autonomous mobile robot capable of right-wall following, PID-based distance control, reflectance line detection, Bluetooth telemetry, and deterministic real-time task scheduling using TI-RTOS on the TI TM4C123G LaunchPad.
---
This repository is structured to support reproducibility for future students and researchers.

## 📦 1. Overview
---
This project contains:

A fully working TI-RTOS application

PID control for right-wall following

Reflectance-based thin/thick line classification

Maze logic (right-turn priority + U-turns)

Ping-pong buffer telemetry

DRV8835 motor driver integration

Sharp IR distance sensors

HC-05 Bluetooth wireless logging

The system uses TI-RTOS Tasks, HWIs, Semaphores, and Clock modules to maintain deterministic timing and modular architecture.

## 🔧 2. Hardware Components (BOM)
---

Component	Qty	Notes

Pololu 5" Round Robot Chassis	1	Base platform

Pololu Micro Metal Gearmotors (100:1)	2	Drive motors

DRV8835 Motor Driver Carrier	1	H-bridge

Pololu 40×7 mm Wheels	1 pair	Motor wheels

Pololu 3/4" Ball Caster	1	Rear support

Sharp GP2Y0A41SK0F (Analog Distance)	2	Right + front

Pololu QTR-1RC Reflectance Sensor	1–2	Line detection

HC-05 Bluetooth Module	1	Serial telemetry

Pololu 6V Regulator (D24V5F6)	1	Motor supply

Pololu 5V Regulator (S7V7F5)	1	Logic supply

TM4C123G LaunchPad	1	MCU

6×AA Battery Pack	1	Power

## 💻 3. Recommended Software Versions
---
Because TI-RTOS support is deprecated in modern CCS releases, the following versions offer the best stability:

Tool	Version

Code Composer Studio (CCS)	6.2 – 7.4 (recommended)

TI-RTOS for TivaC	2.16 – 2.21

XDCtools	3.31 – 3.32

TivaWare	2.1.2.111 or 2.1.4.178

These versions provide reliable kernel builds, functioning .cfg files, and stable driver libraries.

## 📥 4. Installation & Setup
---
### Step 1 — Install Code Composer Studio

Download archived CCS versions:
https://software-dl.ti.com/ccs/esd/documents/ccs-archive.html

Enable during installation:

“Tiva C Series Support”

“TI-RTOS for ARM”

“XDCtools”

### Step 2 — Install TivaWare

Install from TI:
https://www.ti.com/tool/SW-TM4C

Extract into:

C:\ti\TivaWare

### Step 3 — Clone This Repository
git clone https://github.com/ANIL-RONGALA/Autonomous-Maze-Robot-TIRTOS.git

### Step 4 — Import the Project Into CCS
File → Import → CCS Projects → Select Repository Folder


The project will load automatically with the .cfg (RTOS) configuration.

### Step 5 — Connect the Robot Hardware

Attach DRV8835 to motor outputs

Connect Sharp sensors to ADC inputs

Connect QTR sensors to analog pins

Connect HC-05 to UART1 (PC4/PC5 recommended)

Power robot with 6×AA battery pack

### Step 6 — Build and Run
Project → Build → Run → Debug


Open a Bluetooth terminal (9600 baud), pair with HC-05 (1234), and send:

RUN

## 📁 5. Directory Structure
---
```
Autonomous-Maze-Robot-TIRTOS/
│
├── src/
│   ├── FinalProject_TeamXX.c
│   ├── motor.c / motor.h
│   ├── sensors.c / sensors.h
│   ├── pid.c / pid.h
│   ├── bluetooth.c / bluetooth.h
│
├── cfg/
│   ├── system.cfg      # TI-RTOS configuration
│
├── docs/
│   ├── Wiring_Diagram.pdf
│   ├── Architecture_Notes.pdf
│   ├── BOM.pdf
│
└── README.md
```

  
## 🧩 6. System Behavior
---
Autonomous Navigation

Follows right wall at 10 cm distance (PID)

Makes right turns at intersections

Performs U-turns at dead-ends

Stops at thick line, flashes red for 1 minute

Reflectance Line Detection

1st thin line → GREEN LED, start data logging

2nd thin line → BLUE LED, stop logging

Thick line → stop + LED signal

Bluetooth Telemetry

Uses a ping-pong buffer to transmit:

Team 05: 42 36 29 ... 11


Data can be plotted in MATLAB/Python.

## 🔧 7. Recreating Your Own Project
---
Create a new TI-RTOS empty project

Add source files into /src

Add your motor and sensor mappings into motor.h & sensors.h

Configure tasks and HWIs inside .cfg

Build & flash

This repository is designed so any student or researcher can recreate the platform without special hardware modifications.

## 🚀 8. Future Scope & Research Extensions
---
### A. Drone Adaptation

The architecture maps directly into aerial robotics:

PID → altitude/attitude control

Reflectance line → optical flow navigation

DRV8835 PWM → ESC outputs (1–2 ms)

HC-05 → Wi-Fi/ESP-NOW telemetry

Maze → waypoint-based autonomous flight

### B. Multi-Sensor Fusion

Add:

6-axis IMU

Barometer

Magnetometer

Implement:

Extended Kalman Filter

Sensor redundancy

State estimation

### C. Reinforcement Learning

Use RL to learn:

Path optimization

Cornering behavior

Obstacle avoidance

### D. Collaborative Swarm Robots

Enable:

Robot-to-robot communication

Distributed mapping

Swarm decision-making

## 📝 9. Acknowledgments

This project was developed using conventional embedded-systems design practices, TI-RTOS kernel features, control theory, and robotics fundamentals under the guidance of [Dr. Yuha Chen](https://www.ece.uh.edu/faculty/chen-yuhua) & [Dr.Hung Harry Le](https://www.ece.uh.edu/faculty/le-harry) , [Department of Electrical and Computer Engineering](https://www.ece.uh.edu/), [University of Houston](https://www.uh.edu/)

Note:
A small portion of documentation wording was enhanced using AI tools to improve clarity and structure.
All engineering logic, system architecture, and implementation are original.
