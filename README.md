# Bumblebee

Open-source modular autonomous rover chassis based on the Sawppy Rover architecture, redesigned around affordable and locally available hardware in Bangladesh.

## Overview

Bumblebee is a student-led robotics project focused on building a modular autonomous ground rover platform for robotics experimentation, autonomous navigation, and future competition adaptation.

The project is based on the open-source Sawppy Rover by Roger Random, but replaces the original proprietary smart servo drivetrain with a more accessible architecture using DC gear motors and standard PWM servos that are significantly easier to source locally in Bangladesh.

The goal is to explore how advanced open-source robotics platforms can be adapted around affordable and widely available components while remaining modular, extensible, and open-source.

---

## Project Goals

* Build a functional rocker-bogie rover chassis
* Adapt the Sawppy architecture to locally available hardware
* Develop a reusable modular rover platform
* Integrate custom electronics and PCBA
* Experiment with autonomous navigation and ROS 2
* Publicly document the engineering and prototyping process

---

## Key Features

* Rocker-bogie suspension system
* Modular chassis architecture
* Differential steering system
* JGB37-520 DC gear motor drivetrain
* Standard PWM steering servos
* Open-source hardware approach
* Designed for future payload expansion

---

## Why This Build Exists

Many open-source rover platforms rely on expensive or difficult-to-source smart servos and proprietary robotics hardware.

Bumblebee explores how a capable autonomous rover platform can be recreated using affordable and locally accessible components available in Bangladesh while preserving the flexibility and modularity of the original architecture.

This project is also intended to help other students and makers interested in robotics, embedded systems, and autonomous vehicles.

---

## Based on Sawppy Rover

This project is a derivative build based on the Sawppy Rover project by Roger Random.

Original project:

* Sawppy Rover by Roger Random

The original Sawppy architecture, suspension geometry, and open-source design philosophy are fully credited to the Sawppy Rover community.

Bumblebee focuses primarily on:

* drivetrain adaptation,
* hardware localization,
* redesigned mounting systems,
* and future autonomous robotics integration.

---

## Major Changes from Sawppy

| Component         | Sawppy Original        | Bumblebee                          |
| ----------------- | ---------------------- | ---------------------------------- |
| Drive motor       | LX-16A smart servo     | JGB37-520 12V 100RPM DC gear motor |
| Steering          | LX-16A smart servo     | Hiwonder LDX-227 PWM servo         |
| Motor control     | Serial smart servo bus | Standard PWM + motor driver        |
| Servo spline      | Proprietary            | Standard 25T spline                |
| Hardware sourcing | Mostly imported        | Locally available in Bangladesh    |

---

## Current Progress

### Completed

* Chassis architecture finalized
* Hardware selection completed
* Motor mount redesign
* Servo bracket redesign
* Steering linkage adaptation
* STEP file generation
* HCB fiscal sponsorship approved

### In Progress

* Structural component printing
* Electronics planning
* PCBA design
* Chassis assembly

### Planned

* Drivetrain testing
* ROS 2 integration
* Autonomous navigation
* Field testing
* Payload expansion

---

## Hardware Stack

### Mobility

* 6x JGB37-520 12V 100RPM DC gear motors
* 4x Hiwonder LDX-227 PWM servos

### Structure

* Custom 3D printed components
* Aluminum extrusion frame
* Steel/aluminum shafts

### Electronics (Planned)

* Custom motor control PCBA
* Battery power distribution system
* Embedded control system
* Sensor integration

### Software (Planned)

* ROS 2
* Autonomous navigation stack
* Sensor fusion
* Rover control interface

---

Additional files, PCB designs, firmware, and documentation will be added progressively during development.

---

## Open Source

Bumblebee is being developed as an open-source robotics platform.

Modified parts, mounting systems, and future development files will be shared publicly to help other students and makers build similar rover systems using affordable hardware.

---

## Sponsorship

Bumblebee is fiscally sponsored through Hack Club HCB.

We are currently seeking support for:

* PCBA manufacturing
* Robotics hardware
* Drivetrain components
* Sensors and electronics
* 3D printing and prototyping

Sponsor page:
https://adnanosman9.github.io/Bumblebee/sponsor.html

---

## Project Website

https://adnanosman9.github.io/Bumblebee/

---

## Author

Adnan Osman

---

## Acknowledgements

* Roger Random and the Sawppy Rover community
* Hack Club HCB
* Open-source robotics and maker communities
