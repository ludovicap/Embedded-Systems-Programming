# Embedded-Systems-Programming

Adaptive Cruise Control (ACC) – STM32F446RE

Project Overview

This project focuses on the design and implementation of an Adaptive Cruise Control (ACC) system for a robotic vehicle based on the STM32F446RE microcontroller.

The system automatically adjusts the vehicle’s movement according to the distance from an obstacle, using a PID (Proportional–Integral–Derivative) controller.

The main objective is to maintain a predefined reference distance by dynamically adjusting the vehicle’s speed and direction in response to changes in the obstacle’s position.

The firmware is developed in C using STM32CubeIDE, with hardware peripherals primarily configured and managed through direct register-level programming.

Hardware Components

The system consists of the following components:

* STM32F446RE – Microcontroller responsible for data acquisition, processing, and system control.
* HC-SR04 – Ultrasonic sensor used for distance measurement.
* L293D – Motor driver used to control the DC motors.
* DC Motors – Actuators responsible for vehicle movement.
* Battery Power Supply – Enables autonomous operation without a continuous connection to a computer.

System Architecture

The control system operates through the following stages:

1. Distance Measurement: The HC-SR04 ultrasonic sensor measures the distance between the vehicle and the obstacle.
2. Error Calculation: The measured distance is compared with the desired reference distance.
3. PID Control: The controller processes the error and calculates the control output.
4. Motor Control: The control output is converted into a PWM signal to regulate motor speed.
5. Data Logging: The main system variables are stored in the microcontroller’s internal Flash memory.

The overall operation is coordinated by a Finite State Machine (FSM) with three operating states:

* ACC_STOP – Vehicle stopped.
* ACC_FORWARD – Forward movement.
* ACC_BACKWARD – Backward movement.

STM32 Peripherals

GPIO

Digital input/output pins are configured to interface with the ultrasonic sensor and control the motor driver.

Hardware Timers

Hardware timers are used for:

* PWM signal generation.
* Ultrasonic sensor timing measurements.
* System timing and periodic sampling.

Interrupts

Hardware interrupts are used to handle time-sensitive events, reducing the need for blocking operations during firmware execution.

PWM (Pulse Width Modulation)

PWM signals regulate the effective voltage applied to the DC motors, allowing the system to adjust vehicle speed.

USART Communication

The USART peripheral provides serial communication between the STM32 microcontroller and a computer for transferring recorded data.

Internal Flash Memory

System measurements are stored in the microcontroller’s internal Flash memory.

This allows data to be preserved even when the system is powered off and retrieved later for analysis.

PID Controller

The vehicle movement is regulated by a discrete-time PID controller.

The control error is defined as:

[
e(k) = d(k) - d_{ref}
]

where:

* (d(k)) is the measured distance.
* (d_{ref}) is the desired reference distance.
* (e(k)) is the control error at the current sampling instant.

The PID controller calculates the control signal required to reduce the error and maintain the desired distance.

Controller parameters are tuned experimentally by analyzing the vehicle’s response to changes in the obstacle’s position.

Data Acquisition and Analysis

During operation, the firmware records the main system variables:

Variable	Description
time_ms	Sampling timestamp in milliseconds
distance	Measured distance
error	Error relative to the reference distance
uk	PID controller output
pwm	PWM command applied to the motors
state	Current FSM operating state

Data samples are stored in binary format in internal Flash memory, avoiding text conversion during real-time control execution.

After the experiment, the recorded data is transferred to a computer via USART and processed using a Python script.

The Python script uses:

* pyserial for serial communication.
* csv for exporting the recorded measurements.
* matplotlib for data visualization.

The resulting plots allow the analysis of distance measurements, control error, PID output, and PWM commands.

Experimental Procedure

The system is evaluated through a sequence of experimental tests:

1. The vehicle approaches a stationary obstacle.
2. When the reference distance is reached, the controller adjusts the motor commands until the vehicle stops.
3. The obstacle is moved forward, and the vehicle responds by moving forward to restore the desired distance.
4. The obstacle is moved closer, and the vehicle responds by moving backward.

The recorded measurements are used to evaluate the dynamic response of the system and support PID parameter tuning.

Technologies and Development Tools

* Programming Language: C
* Microcontroller: STM32F446RE
* Development Environment: STM32CubeIDE
* Embedded Programming: Register-level peripheral configuration
* Control Strategy: Discrete PID and Finite State Machine
* Motor Control: PWM
* Communication Interface: USART
* Data Storage: Internal Flash memory
* Data Processing: Python, PySerial, CSV, Matplotlib

Educational Objectives

The project was developed to explore the design and implementation of embedded control systems, with particular emphasis on:

* STM32 peripheral configuration and register-level programming.
* Hardware timer and interrupt management.
* Real-time digital control implementation.
* DC motor control using PWM.
* Persistent data logging in internal Flash memory.
* Serial communication between embedded hardware and a computer.
* Experimental analysis and tuning of a PID controller.

Documentation

The complete technical documentation provides further details about the hardware and software architecture, peripheral configuration, implementation choices, and experimental evaluation of the control system.
