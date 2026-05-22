# Bumblebee Rover

[![License: CERN-OHL-S-2.0](https://img.shields.io/badge/Hardware-CERN--OHL--S--2.0-blue.svg)](https://ohwr.org/cern_ohl_s_v2.txt)
[![Fiscal Sponsor: HCB](https://img.shields.io/badge/Fiscal%20Sponsor-Hack%20Club%20HCB-ec3750.svg)](https://hcb.hackclub.com/donations/start/bumblebee)
[![Status: Active](https://img.shields.io/badge/Status-Active%20Build-22c55e.svg)](#current-progress)
[![Open Source Hardware](https://img.shields.io/badge/Open%20Source-Hardware-orange.svg)](https://www.oshwa.org/)

Open-source modular autonomous rover chassis based on the [Sawppy Rover](https://github.com/Roger-random/Sawppy_Rover) architecture by [@Roger-random](https://github.com/Roger-random), redesigned around affordable and locally available hardware in Bangladesh.

---

## Overview

This is a student-led robotics project building a modular autonomous ground rover platform for robotics experimentation, autonomous navigation, and future competition adaptation.

Bumblebee is a derivative of the Sawppy Rover by Roger Random, replacing the original LX-16A smart servo drivetrain with JGB37-520 DC gear motors and Hiwonder LDX-227 PWM servos — components that are significantly easier to source locally in Bangladesh at a fraction of the cost. Everything is open-source: CAD files, schematics, BOM, and build logs are published here as development progresses.

---

## Project Goals

- Build a functional rocker-bogie rover chassis adapted for local hardware
- Develop a reusable, modular rover platform for robotics experimentation
- Integrate ROS 2 for autonomous navigation and sensor fusion
- Publicly document the full engineering and prototyping process for other students and makers

---

## Key Features

- Rocker-bogie suspension system (Sawppy geometry, adapted mounts)
- Modular chassis architecture designed for payload expansion
- JGB37-520 12V 100RPM DC gear motor drivetrain (×6)
- Hiwonder LDX-227 PWM servo steering (×4)
- Standard 25T servo spline — no proprietary hardware
- Designed for ROS 2 integration and future autonomous navigation stack

---

## Major Changes from Sawppy

| Component | Sawppy Original | Bumblebee |
|---|---|---|
| Drive motor | LX-16A smart servo | JGB37-520 12V 100RPM DC gear motor |
| Steering | LX-16A smart servo | Hiwonder LDX-227 PWM servo |
| Motor control | Serial smart servo bus | BTS7960 |
| Servo spline | Proprietary | Standard 25T spline |
| Control MCU | — | Arduino or ESP |
| single board computer | — | Raspberry pi 4 4B |
| IMU | — | MPU-6050 |
| Hardware sourcing | Mostly imported | Locally available in Bangladesh |

---

## Hardware Stack

### Mobility
- 6× JGB37-520 12V 100RPM DC gear motors
- 4× Hiwonder LDX-227 PWM servos
- BTS7960 motor driver

### Structure
- Custom 3D printed components (PLA/PETG, ~3 kg)
- Aluminum extrusion frame
- Steel/aluminum shafts

### Electronics
- Raspberry pi 4
- Arduino or ESP
- MPU-6050 IMU
- LiPo battery pack + BMS

### Software (Planned)
- ROS 2
- Autonomous navigation stack (GPS waypoints + SLAM)
- Sensor fusion
- Rover control interface

---

## Current Progress

### Completed
- Chassis architecture finalized
- Hardware selection completed
- Motor mount redesign
- Servo bracket redesign
- Steering linkage adaptation
- STEP files generated — available in [`/cad`](./cad)
- BOM completed
- Build log available on 
- HCB fiscal sponsorship approved

### In Progress
- Structural component printing
- Chassis assembly

### Planned
- Drivetrain testing
- ROS 2 integration
- Autonomous navigation
- Field testing
- Payload expansion

---

## Why This Build Exists

Most capable open-source rover platforms — including the original Sawppy — rely on LX-16A or similar smart servos that are expensive and difficult to source reliably outside of the US, Europe, or China. Bumblebee is a direct answer to that problem: a full rocker-bogie rover platform rebuilt around hardware that is actually available in Bangladesh, at prices students can work with.

The engineering tradeoffs are documented openly. This project is also intended to help other students and makers in similar situations adapt advanced robotics platforms to their local hardware ecosystem.

---

## Sponsorship

Bumblebee is fiscally sponsored by [Hack Club](https://hackclub.com), a 501(c)(3) nonprofit (EIN 81-2908499). **US donations are tax-deductible.**

We are currently seeking support for:

| What | Why it matters |
|---|---|
| PCBA fabrication | KiCad files are ready — manufacturing is the only blocker |
| 3D printing | Structural parts, FDM in PLA/PETG |
| JGB37-520 motors + LDX-227 servos | Hard to source at consistent spec in Bangladesh |
| Sensors & compute | IMU, GPS, SBC for autonomous navigation stack |

**→ [Sponsor page](https://adnanosman9.github.io/Bumblebee/sponsor.html)**
**→ [Donate directly via HCB](https://hcb.hackclub.com/donations/start/bumblebee)**

Sponsors receive logo placement on the project website and permanent credit in all documentation.

---

## Repository Structure

```
/
├── cad/          # Fusion 360 source files and STEP exports
├── pcb/          # KiCad schematics and PCB layouts
├── firmware/     # ESP32 firmware (in progress)
├── docs/         # Build logs and engineering notes
└── bom/          # Bill of materials
```

---

## License

Hardware designs in this repository are licensed under the **CERN Open Hardware Licence Version 2 - Strongly Reciprocal (CERN-OHL-S-2.0)**.

You are free to use, study, modify, and distribute this hardware and its documentation, provided that derivatives are released under the same license.

See [`LICENSE`](./LICENSE) for the full text, or visit [ohwr.org/cern_ohl_s_v2.txt](https://ohwr.org/cern_ohl_s_v2.txt).

---

## Acknowledgements

- [Roger Random (@Roger-random)](https://github.com/Roger-random) and the [Sawppy Rover](https://github.com/Roger-random/Sawppy_Rover) community — original architecture, suspension geometry, and open-source design philosophy
- [Hack Club HCB](https://hackclub.com/hcb) — fiscal sponsorship
- Open-source robotics and maker communities

---

## Author

**Adnan Osman** — [github.com/Adnanosman9](https://github.com/Adnanosman9)

Project website: [adnanosman9.github.io/Bumblebee](https://adnanosman9.github.io/Bumblebee/)
