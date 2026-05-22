# Architecture Journal  Bumblebee Rover

> This document records every major hardware decision made during the Bumblebee build  why we chose what we chose, why we rejected the alternatives, and what to do if you can't find the exact part. Written for builders in Bangladesh and similar hardware-constrained environments.

---

## 1. Drive Motor  JGB37-520 12V 100RPM DC Gear Motor

### Why this
The JGB37-520 is a metal-gearbox DC gear motor with a D-shaft output, widely available in Bangladesh from local electronics markets and online sellers. At 12V 100RPM it delivers enough torque to move a ~5kg rover chassis over uneven ground without stalling. The D-shaft is straightforward to couple to printed hubs. It is robust, repairable, and cheap enough to replace if one fails during testing.

### Why not the original (LX-16A Smart Servo)
The LX-16A is a serial bus smart servo that handles both drive and steering in the original Sawppy. It requires a proprietary TTL serial protocol, a specific controller board, and is expensive and difficult to source in Bangladesh. A single LX-16A costs more than the entire JGB37-520 drivetrain for this build. It also means 10 identical units for a 6-wheel drive + 4-steering configuration  the import cost alone makes it impractical.

### Why not other available options
- **Standard DC hobby motors (no gearbox)**  not enough torque at rover wheel speeds without external gearing. Would require additional mechanical complexity.
- **Stepper motors**  too heavy, inefficient for continuous rotation, overkill for this application, hard to source in the right form factor locally.
- **Worm gear motors**  self-locking behavior makes them unsuitable for a suspension system that needs to absorb terrain impacts through the drivetrain.
- **High-RPM DC motors with encoder**  RPM too high, torque too low without significant reduction gearing.

### If you can't find the JGB37-520
You need a **DC gear motor** with the following minimum specifications:

| Specification | Minimum | Recommended |
|---|---|---|
| Voltage | 6V | 12V |
| No-load speed | 50 RPM | 80–120 RPM |
| Stall torque | 5 kg·cm | 8–15 kg·cm |
| Shaft type | D-shaft or round with flat | D-shaft preferred |
| Shaft diameter | 6mm | 6mm |
| Body diameter | 37mm class | 37mm (fits existing mounts) |
| Gearbox | Metal | Metal (plastic will strip under load) |

Search for: **N20, N30, JGA25, GA25, JGB37 series** gear motors at your local electronics market. If the body diameter differs from 37mm you will need to reprint the motor brackets  the STEP files are parametric enough to adapt. Avoid motors with plastic gearboxes; they will strip under stall load.

---

## 2. Steering  Hiwonder LDX-277 PWM Servo

### Why this
Standard 25T spline PWM servo with enough torque to hold steering position under load. Compatible with every standard servo controller and the ESP32-C3 PWM output directly. The 25T spline is an industry standard  servo horns, couplers, and brackets are interchangeable with dozens of other brands. LDX-277 is sourceable in Bangladesh and the torque-to-cost ratio is good for this application.

### Why not the original (LX-16A Smart Servo)
Same reasons as drive  serial bus protocol, expensive, import-only, proprietary ecosystem.

### Why not other available options
- **MG996R / MG995**  very common and cheap, but torque rating is often inflated by manufacturers. Plastic gears in some variants. Acceptable as a fallback but not first choice.
- **Digital servos (high-end)**  unnecessary precision and cost for a steering application that only needs four positions (left, center-left, center-right, right range).
- **Linear actuators**  too slow for real-time steering response and mechanically complex to integrate into the existing knuckle geometry.

### If you can't find the LDX-277
You need a **standard PWM servo** with the following minimum specifications:

| Specification | Minimum | Recommended |
|---|---|---|
| Torque | 10 kg·cm | 15–20 kg·cm |
| Spline | 25T standard | 25T standard |
| Voltage | 5V | 6–7.4V |
| Protocol | PWM (50Hz) | PWM (50Hz) |
| Gear material | Metal | Metal |
| Body width | ~40mm | Standard servo form factor |

Search for: **MG996R, DS3218, LX-225, Hitec HS-485HB** or any servo labeled "25T metal gear standard size." If torque is below 10 kg·cm the servo will skip under cornering load. The 25T spline is critical  if you use a servo with a different spline count (for example 24T or 23T) the printed couplers will not fit and you will need to reprint them.

---

## 3. Motor Driver  BTS7960 43A H-Bridge Module

### Why this
The BTS7960 is a high-current half-bridge driver chip. On a module it forms a full H-bridge capable of 43A peak, 14A continuous per channel. The JGB37-520 can draw 5–10A at stall  the BTS7960 handles this without browning out or burning. Standard PWM input, 12V compatible, available in Bangladesh, and cheap. Three modules handle all six drive motors in pairs (front pair, middle pair, rear pair).

### Why not DRV8833
The DRV8833 is a dual H-bridge rated at 1.5A continuous, 2A peak per channel. The JGB37-520 stall current exceeds this by a factor of 3–5×. Under real terrain load the DRV8833 would trigger thermal shutdown or burn out. It is the right choice for small hobby motors but wrong for this drivetrain.

### Why not other available options
- **L298N**  old design, very inefficient (up to 3V drop across the driver), runs extremely hot, wastes battery. Functional but wasteful.
- **L293D**  600mA per channel, completely insufficient for this application.
- **IBT-2 module**  essentially the same as BTS7960 (same chip), just a different PCB layout. Fully compatible substitute.
- **Sabertooth / Kangaroo**  capable but expensive, overkill, and harder to source locally.

### If you can't find the BTS7960
You need a **motor driver module** with the following minimum specifications:

| Specification | Minimum | Recommended |
|---|---|---|
| Continuous current per channel | 10A | 15A+ |
| Peak current per channel | 20A | 43A |
| Operating voltage | 12V | 6–27V range |
| Input signal | PWM | PWM (3.3V logic compatible) |
| Heat dissipation | Heatsink required | Heatsink + airflow |

Direct substitute: **IBT-2 module** (identical chip, different board layout  fully pin-compatible).
Acceptable fallback: **L298N** (inefficient but functional  expect heat and reduced battery life).
Search for: BTS7960, IBT-2, "43A motor driver module" on local markets or AliExpress.

Wiring note: 3 drivers for 6 motors. Each driver uses 4 GPIO pins (RPWM, LPWM, R_EN, L_EN). Total GPIO used for drive: **12 pins** from the ESP32-C3.

---

## 4. Low-Level MCU  XIAO ESP32-C3 (or Arduino fallback)

### Why this
The XIAO ESP32-C3 is a compact, low-cost microcontroller with enough GPIO for PWM servo control, motor driver signals, and IMU communication over I2C. It handles the real-time control loop: reading the MPU-6050, outputting PWM to servos, sending PWM + enable signals to the BTS7960 drivers, and communicating with the Raspberry Pi over UART or USB serial. Small footprint, 3.3V logic (compatible with BTS7960 input), Wi-Fi capable for debugging.

### Why not Arduino Uno / Nano
Arduino is a completely valid fallback and simpler to program for beginners. The Uno/Nano runs at 5V logic which requires level shifting to interface with 3.3V peripherals. It has fewer GPIO pins and no Wi-Fi. For the basic control loop it works fine  it just needs a logic level converter between the Arduino and the BTS7960 if using a 5V board.

**Arduino is the recommended fallback** if you cannot source the XIAO ESP32-C3 or are not comfortable with ESP-IDF / Arduino-ESP32 framework.

### Why not other available options
- **STM32 Bluepill**  capable but complex toolchain setup, harder to find working USB bootloaders locally, steeper learning curve.
- **Teensy**  excellent but expensive and import-only in Bangladesh.
- **Raspberry Pi Pico**  good alternative, 3.3V logic, dual-core, MicroPython or C SDK. Viable substitute if ESP32-C3 is unavailable.
- **NodeMCU ESP8266**  lacks enough GPIO for this application (6 motor driver signals + 4 servo signals + I2C = tight), and no hardware PWM on enough pins.

### If you can't find the XIAO ESP32-C3
You need a **microcontroller** with the following minimum specifications:

| Specification | Minimum | Recommended |
|---|---|---|
| PWM-capable GPIO pins | 16 | 20+ |
| I2C | 1 bus | 1 bus |
| UART | 1 port | 1 port (for Pi communication) |
| Logic voltage | 3.3V or 5V | 3.3V (check BTS7960 input spec) |
| Clock speed | 16 MHz | 80–240 MHz |

Acceptable substitutes in order of preference:
1. **Arduino Mega 2560**  most GPIO, easy to source, 5V (use level shifter for BTS7960)
2. **Raspberry Pi Pico**  3.3V, dual-core, MicroPython friendly
3. **Arduino Uno/Nano**  limited pins but works for basic control loop
4. **ESP32 DevKit (30-pin)**  direct ESP32 family substitute, more GPIO than XIAO

---

## 5. Single Board Computer  Raspberry Pi (any model 3B+, 4, or Zero 2W)

### Why this
The Raspberry Pi runs the high-level autonomy stack: ROS 2, GPS navigation, SLAM, camera processing, and mission planning. It communicates with the ESP32-C3 (low-level MCU) over UART or USB serial  the Pi sends movement commands, the ESP32 executes them in real time. This separation keeps the real-time control loop on dedicated hardware and the compute-heavy autonomy stack on Linux.

### Why not run everything on the Pi
The Raspberry Pi Linux OS is not a real-time operating system. PWM timing, motor control loops, and servo signals require microsecond-level precision that Linux cannot guarantee. Running motor drivers directly from Pi GPIO is unreliable under CPU load. The ESP32-C3 handles everything time-critical; the Pi handles everything compute-heavy.

### Why not other available options
- **Jetson Nano**  more powerful for computer vision and ML inference, but expensive, harder to source in Bangladesh, and overkill for initial navigation stack.
- **Orange Pi / Banana Pi**  viable substitutes if Raspberry Pi is unavailable. ROS 2 support is less mature but workable on Ubuntu ARM builds.
- **Beaglebone Black**  real-time PRU cores are interesting but ROS 2 ecosystem support is weaker.
- **Old laptop/PC**  too heavy, too power-hungry for a rover platform.

### If you can't find a Raspberry Pi
You need a **single board computer** with the following minimum specifications:

| Specification | Minimum | Recommended |
|---|---|---|
| CPU | Quad-core ARM Cortex-A | Cortex-A53 or better |
| RAM | 1 GB | 2–4 GB |
| OS | Linux (Ubuntu/Debian ARM) | Ubuntu 22.04 ARM |
| USB | 1× USB 2.0 | 2× USB |
| UART / GPIO | Available | For ESP32 communication |
| Power consumption | <10W | <8W |

Acceptable substitutes:
1. **Orange Pi 3 LTS / Orange Pi 5**  good ROS 2 support, available in Bangladesh
2. **Radxa Rock 3**  Ubuntu support, similar form factor
3. **Raspberry Pi Zero 2W**  lower power, less RAM, still runs ROS 2 lite
4. Any SBC running **Ubuntu 22.04 ARM** with ROS 2 Humble packages available

---

## 6. IMU  MPU-6050

### Why this
6-axis IMU (3-axis accelerometer + 3-axis gyroscope) over I2C. Cheap, universally available everywhere in Bangladesh, well-supported in every Arduino and ESP32 library ecosystem. Sufficient for basic orientation estimation and tilt detection on the rover.

### Why not other available options
- **MPU-9250**  adds magnetometer, better for absolute heading but harder to source and more expensive. Upgrade path, not necessary for initial build.
- **BNO055**  has onboard sensor fusion which simplifies firmware but costs significantly more.
- **ADXL345 (accelerometer only)**  no gyro, insufficient for dynamic orientation estimation.

### If you can't find the MPU-6050
Any **I2C IMU module** with the following:

| Specification | Minimum |
|---|---|
| Axes | 6DOF (accel + gyro) |
| Interface | I2C |
| Voltage | 3.3V or 5V with onboard regulator |
| Library support | Arduino / ESP32 compatible |

Substitutes: **MPU-9250, GY-521 (same chip as MPU-6050), ICM-20600, LSM6DS3**. The GY-521 module IS the MPU-6050 on a breakout board  they are the same thing with different labels.

---

## Decision Summary

| Component | Chosen | Rejected | Key reason |
|---|---|---|---|
| Drive motor | JGB37-520 | LX-16A smart servo | Cost, local availability, D-shaft simplicity |
| Steering | LDX-277 PWM servo | LX-16A smart servo | Standard 25T spline, PWM compatible |
| Motor driver | BTS7960 | DRV8833, L298N | Stall current handling (43A peak) |
| Low-level MCU | XIAO ESP32-C3 | Arduino Uno, STM32 | GPIO count, 3.3V logic, compact size |
| MCU fallback | Arduino Mega |  | Easy to source, simple toolchain |
| SBC | Raspberry Pi | Jetson Nano, Orange Pi | ROS 2 ecosystem, local availability |
| IMU | MPU-6050 | BNO055, MPU-9250 | Universal availability, I2C, cheap |

---

*Last updated: May 2026*
*Bumblebee is fiscally sponsored by [Hack Club HCB](https://hcb.hackclub.com/donations/start/bumblebee) · 501(c)(3) · EIN 81-2908499*
