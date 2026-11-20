# Embedded-Systems-Programming

🚗 Adaptive Cruise Control | STM32

A real-time embedded control system for autonomous distance regulation using STM32F446RE and PID control.

⸻

📌 Overview

This project presents the development of an Adaptive Cruise Control (ACC) system implemented on an STM32F446RE microcontroller.

The system enables a robotic vehicle to automatically adjust its speed and direction to maintain a desired distance from an obstacle.

A discrete PID controller processes real-time distance measurements, while a Finite State Machine (FSM) manages forward movement, backward movement, and stopping.

The firmware is written in C, with a focus on low-level peripheral configuration, interrupt-driven operations, and real-time control.

⚙️ How It Works

The control loop follows five main steps:

Distance Sensing → Error Calculation → PID Control → PWM Generation → Motor Actuation

1. The HC-SR04 ultrasonic sensor measures the distance to an obstacle.
2. The measured distance is compared with a predefined reference.
3. The PID controller calculates the required control action.
4. PWM signals regulate the speed of the DC motors.
5. The FSM determines the appropriate movement direction.

Finite State Machine

State	Behavior
ACC_FORWARD	Moves toward the obstacle
ACC_STOP	Stops when the target distance is reached
ACC_BACKWARD	Moves away from the obstacle

🔧 Hardware Setup

Component	Purpose
STM32F446RE	Main processing and control unit
HC-SR04	Ultrasonic distance measurement
L293D	DC motor driver
DC Motors	Vehicle actuation
Battery Supply	Standalone operation

💻 Firmware & Peripherals

The firmware integrates several STM32 hardware resources:

* GPIO – Sensor interfacing and motor direction control
* Timers – PWM generation, timing, and periodic sampling
* Interrupts – Event-driven hardware management
* USART – Serial data communication
* Internal Flash – Persistent storage of experimental measurements

Peripheral management is primarily implemented through direct register-level programming.

📊 Data Logging & Analysis

The system includes a data acquisition framework for evaluating controller performance.

During operation, measurements are stored in the STM32’s internal Flash memory, allowing the vehicle to operate independently from the computer.

After each experiment, the recorded data can be retrieved through USART and processed using Python.

Recorded variables:

time_ms · distance · error · uk · pwm · state

Python tools:

* pyserial – Serial data acquisition
* csv – Data export
* matplotlib – Experimental data visualization

The resulting plots support the analysis of the vehicle’s dynamic response and the experimental tuning of the PID controller.

🧪 Experimental Validation

The system is tested under different obstacle movements to evaluate its ability to maintain the reference distance.

The experimental sequence includes:

1. Approaching a stationary obstacle.
2. Stopping near the desired reference distance.
3. Following an obstacle moving away.
4. Moving backward when the obstacle approaches.

These tests provide insight into the controller’s responsiveness, stability, and tracking performance.

🛠️ Tech Stack

Embedded Development

C · STM32CubeIDE · STM32F446RE · Register-Level Programming

Control & Hardware

PID · FSM · PWM · Timers · Interrupts · USART · Flash Memory

Data Analysis

Python · PySerial · CSV · Matplotlib

⸻

🎯 Project Goals

* Develop a real-time embedded control application.
* Implement a discrete PID controller for distance regulation.
* Interface sensors and actuators through STM32 peripherals.
* Manage hardware events using interrupts.
* Implement persistent data logging.
* Analyze experimental results using Python.

⸻

📚 Documentation

Detailed information about the system architecture, firmware implementation, peripheral configuration, and experimental results is available in the project documentation.

⸻

Embedded Systems Project | STM32F446RE · PID Control · Real-Time Systems
