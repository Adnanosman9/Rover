# Bill of Materials of Bumblebee Rover

> Based on the [Sawppy Rover](https://github.com/Roger-random/Sawppy_Rover) architecture by [@Roger-random](https://github.com/Roger-random), adapted for locally available hardware in Bangladesh.

---

## Printed Parts
~3 kg total filament (PLA or PETG)

| Qty | Part | Notes |
|-----|------|-------|
| 88 | Clip2n125 | Print extra for spares |
| 12 | Clip3n20 | Print extra for spares |
| 6 | Wheel Hub | Modified for JGB37-520 D-shaft |
| 6 | JGB37-520 Motor Bracket | Redesigned mount |
| 6 | JGB37-520 Motor Coupler | Wheel-to-motor connection |
| 4 | LDX-277 Coupler | Redesigned for 25T spline |
| 4 | LDX-277 Bracket | Redesigned for servo dimensions |
| 6 | Wheel | |
| 4 | Steering Knuckle | Modified geometry |
| 4 | Body Corner | |
| 2 | DiffBrace / DiffLink | |
| 1 | DiffLower / DiffUpper | |
| 2 | Rod Support | |
| 1 | Power Panel | Updated for new electronics layout |
| 2 ea | Fixed Knuckle, Front Knuckle, Rear Knuckle | Mirrored pairs |
| 2 ea | Bogie Wheels, Bogie Body | Mirrored pairs |
| 2 ea | Rocker, Rocker Body Mount | Mirrored pairs |
| 2 ea | DiffEnd, Battery Tray | Mirrored pairs |

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

- **LDX-277 vs LDX-227** - verify exact model number before ordering. The website uses LDX-277; the README previously referenced LDX-227. Check your supplier listing.
- **BTS7960 wiring** - 3 drivers handle 6 motors in pairs (left-front+right-front, left-mid+right-mid, left-rear+right-rear). Each driver needs RPWM, LPWM, R_EN, and L_EN.
- **608 bearings** - standard inline skate bearings, widely available locally.
- Printed part STEP files: [`/Step-files`](./Step-files)

---

*Bumblebee is fiscally sponsored by [Hack Club HCB](https://hcb.hackclub.com/donations/start/bumblebee) (501(c)(3) · EIN 81-2908499). Manufacturing sponsorships welcome — [sponsor page](https://adnanosman9.github.io/Bumblebee/sponsor.html).*
