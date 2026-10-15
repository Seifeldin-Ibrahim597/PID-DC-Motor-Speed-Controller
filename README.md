# PID-DC-Motor-Speed-Controller
Design and development of a PID-based DC motor speed control system using MATLAB/Simulink and hardware testing.
# PID Speed and Position Controller for a DC Motor

## Project Overview

This project aims to design, simulate, and implement a PID (Proportional-Integral-Derivative) controller to regulate the speed of a DC motor.

The main objective is to develop a control system capable of maintaining a desired motor speed, responding to changes in speed commands, and compensating for external disturbances.

The project will combine MATLAB/Simulink modelling, Arduino programming, and physical hardware testing to explore real-world control systems engineering.

## Project Objectives

- Develop a mathematical model of a DC motor.
- Design and tune a PID controller using MATLAB/Simulink.
- Implement the controller on an Arduino microcontroller.
- Measure motor speed using a quadrature encoder.
- Compare simulation results against experimental measurements.
- Evaluate system performance using overshoot, settling time, rise time, and steady-state error.
- Explore position control as a potential extension.

## Planned Hardware

| Component | Purpose |
|---|---|
| Arduino Uno R4 or Nano | Runs the control algorithm |
| 12V DC geared motor with quadrature encoder | Motor being controlled and measured |
| TB6612FNG motor driver | Controls motor power and direction |
| 12V 2A power supply | Supplies the motor |
| 10kΩ potentiometer | Adjusts the desired motor speed |
| 100µF capacitor | Helps stabilise the motor supply |

## Software and Tools

- **MATLAB/Simulink:** System modelling, simulation, and PID tuning.
- **Arduino IDE / C++:** Implementing the control algorithm.
- **Python:** Recording, processing, and plotting experimental data.
- **GitHub:** Version control and technical documentation.
- **Wokwi:** Initial circuit and encoder simulations.

## Planned Development Stages

1. Learn PID control principles and embedded programming fundamentals.
2. Assemble the motor, driver, encoder, and Arduino.
3. Test motor operation and encoder measurements.
4. Identify the motor's dynamic behaviour using experimental data.
5. Develop and tune a PID controller in MATLAB/Simulink.
6. Implement the controller on Arduino.
7. Evaluate and compare experimental and simulated results.
8. Investigate potential position-control improvements.

## Current Progress

**Status: Planning and preparation**

The initial project scope, proposed hardware, software requirements, and development stages have been defined.

The next steps are to complete introductory control systems training, obtain the required components, and begin encoder simulation.

Experimental results, code, plots, and photographs will be added as the project progresses.

## Expected Outcome

The intended outcome is a functioning closed-loop DC motor controller supported by documented test results, simulation comparisons, and an evaluation of the system's limitations.

This project is part of my engineering portfolio, focusing on control systems, embedded programming, and model-based design.
