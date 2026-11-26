# PID-DC-Motor-Speed-Controller project demo
https://github.com/user-attachments/assets/32b94288-672a-4bc1-9e9b-1e3ab4dba8d7

# PID DC Motor Speed Controller

**Project Status: Completed**

## Project Overview

This project involved designing and developing a closed-loop PID (Proportional–Integral–Derivative) control system for regulating the rotational speed of a DC motor using an Arduino Nano ESP32.

The system uses a potentiometer to define the desired motor speed and a quadrature encoder to measure the actual rotational speed. The PID controller continuously calculates the difference between the desired and measured speed, adjusting the PWM output to the motor driver to regulate motor performance.

## Hardware and Components

| Component | Purpose |
|---|---|
| Arduino Nano ESP32 | Main microcontroller and PID processing |
| L298N motor driver | Motor direction and speed control |
| DC geared motor | Mechanical output |
| Quadrature encoder | Real-time rotational speed measurement |
| 10 kΩ potentiometer | Adjustable speed setpoint |
| External 12V power supply | Motor power supply |
| Breadboard | Circuit prototyping |
| Jumper wires | Electrical connections |
| USB cable | Programming and microcontroller power |

## Software and Technologies

- Arduino IDE
- C/C++ programming
- PID control algorithms
- Pulse Width Modulation (PWM)
- Quadrature encoder feedback
- Interrupt-based signal processing
- Analogue-to-digital conversion (ADC)
- Real-time serial monitoring

## Completed Development Stages

- [x] Research into PID and closed-loop control systems
- [x] Hardware selection and component acquisition
- [x] Motor driver integration
- [x] Quadrature encoder integration
- [x] Potentiometer-based speed adjustment
- [x] PWM motor speed control
- [x] PID algorithm implementation
- [x] Hardware and software integration
- [x] Physical prototype assembly
- [x] Functional demonstration
- [x] Source code documentation
- [x] Wiring diagram development

## Engineering Skills Developed

- Control systems engineering
- Embedded systems programming
- Electrical circuit design
- Electromechanical system integration
- Sensor feedback and signal processing
- Motor control and automation
- Hardware troubleshooting and debugging
- Technical documentation
- Rapid prototyping

## Future Improvements

Although the initial prototype is complete, further development could include:

- Experimental optimisation of PID gains.
- MATLAB and Simulink system modelling.
- Quantitative analysis of overshoot, settling time and steady-state error.
- Automatic disturbance rejection testing.
- OLED display integration.
- Custom PCB design.
- Integration into a larger robotic or industrial automation system.

## Project Outcome

The completed prototype demonstrates the practical integration of mechanical, electrical and software engineering principles into a functional motor control system. It provides a foundation for more advanced projects in robotics, mechatronics, industrial automation and intelligent control systems.
