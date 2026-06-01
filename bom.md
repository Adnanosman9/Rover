# Bill of Materials — Bumblebee Rover

> Based on the [Sawppy Rover](https://github.com/Roger-random/Sawppy_Rover) architecture by [@Roger-random](https://github.com/Roger-random), adapted for locally available hardware in Bangladesh.

---

## Printed Parts
~3 kg total filament (PLA or PETG)

| Qty | Part | Notes |
|-----|------|-------|
| 88 | Clip2n125 | Print a few extra for spares |
| 12 | Clip3n20 | Print a few extra for spares |
| 6 | Wheel Hub | Print a few extra for spares |
| 4 | Servo Coupler | Print a few extra for spares |
| 4 | Servo Bracket | |
| 6 | Wheel | |
| 4 | Steering Knuckle | |
| 4 | Body Corner | |
| 2 | DiffBrace | |
| 2 | DiffLink | |
| 1 | DiffLower | |
| 1 | DiffUpper | |
| 2 | Rod Support | |
| 1 | Power Panel | |
| 2 | Fixed Knuckle | Mirrored |
| 2 | Front Corner | Mirrored |
| 2 | Rear Corner | Mirrored |
| 2 | Bogie Wheels | Mirrored |
| 2 | Bogie Body | Mirrored |
| 2 | Rocker | Mirrored |
| 2 | Rocker Body Mount | Mirrored |
| 2 | DiffEnd | Mirrored |
| 2 | Battery Tray | Mirrored |
| 6 | JGB37-520 Motor Bracket | Redesigned mount · not yet designed, pending physical measurements |
| 6 | JGB37-520 Motor Coupler | Wheel-to-motor connection · not yet designed, pending physical measurements |

---

## Shafts
Steel for differential shaft. Aluminum or steel for all others.

| Qty | Length (mm) | Part |
|-----|-------------|------|
| 1 | 300 | Differential Shaft |
| 6 | 50 | Wheel Axle Shaft |
| 4 | 61 | Steering Shaft |
| 2 | 66.5 | Suspension Bogie Pivot |
| 2 | 84 | Suspension Rocker Pivot |

---

## Hardware & Electronics

| Qty | Part | Notes |
|-----|------|-------|
| 6 | JGB37-520 12V 100RPM DC Gear Motor | Drive |
| 4 | Hiwonder LDX-277 PWM Servo | Steering |
| 6 | Motor Shaft Couplers | JGB37-520 D-shaft compatible |
| 3 | BTS7960 43A Motor Driver Module | Paired motors per driver (2 motors × 3 drivers) |
| 1 | XIAO ESP32-C3 | Main control MCU |
| 1 | MPU-6050 | IMU |
| 1 | 12V LiPo Battery Pack | |
| 1 | Battery Management System (BMS) | 12V compatible |
| 30 | 608 Bearings | |
| 300 | M3×8mm Socket Head Screws | |
| 28 | M3×16mm Socket Head Screws | |
| 300 | M3 Washers + Nuts | |
| 100 | M3 Threaded Inserts | |
| 100 | 5/16" E-Clips | |
| 22 | M3×8 Set Screws | |
| 2 | Turnbuckles | Steering linkage |
| 40 | 1/4" Brass Screws | |

---

## Aluminum Extrusion
Standard 15mm or 20mm V-slot / T-slot profile.

| Qty | Length (mm) | Purpose |
|-----|-------------|---------|
| 4 | 385 | Main body, lengthwise |
| 4 | 245 | Main body, widthwise |
| 1 | 238 | Differential fixed beam |
| 2 | 182 | Rocker joint to front wheel |
| 2 | 161 | Rocker joint to bogie joint |
| 2 | 122 | Bogie joint to middle wheel |
| 2 | 117 | Bogie joint to rear wheel |

---

## Notes

- **Motor Bracket & Coupler** — not yet designed. Will be modeled after physical parts are printed and measured.
- **BTS7960 wiring** — 3 drivers handle 6 motors in pairs (left-front+right-front, left-mid+right-mid, left-rear+right-rear). Each driver needs RPWM, LPWM, R_EN, L_EN from the ESP32-C3 — 12 GPIO pins total for drive.
- **608 bearings** — standard inline skate bearings, widely available locally.
- Printed part STEP files: [`/cad`](./cad)

---

*Bumblebee is fiscally sponsored by [Hack Club HCB](https://hcb.hackclub.com/donations/start/bumblebee) (501(c)(3) · EIN 81-2908499). Manufacturing sponsorships welcome — [sponsor page](https://adnanosman9.github.io/Bumblebee/sponsor.html).*
