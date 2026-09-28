# IoT Lab 8: Motor Control & Actuation


## 📋 Course Information

- **Course:** Internet of Things (IoT) Lab
- **Instructor:** Vipul Singh Negi


---

## 📑 Overview & Theory

Motors are key output devices (actuators) in IoT and robotic systems, enabling physical motion based on sensor inputs and controller logic.

### Types of Motors Covered

| Motor Type | Description | Key Features |
| :--- | :--- | :--- |
| **DC Motor** | Direct Current motor, most basic electric motor type. | 2 leads (Positive/Negative). Reversing polarity changes rotation direction. Continuous rotation. |
| **Servo Motor** | Rotary or linear actuator with position feedback. | Precise control of angular/linear position, velocity, and acceleration. Requires a sensor and controller module. |
| **Stepper Motor** | Brushless DC motor dividing full rotation into equal steps. | Moves and holds position in incremental steps without feedback sensors (open-loop control). |

---

## ⚙️ Stepper Motor Deep Dive

### Working Configurations & Stator Windings
- **Permanent Magnet Stepper Motor:** Uses a permanent magnet rotor driven by electromagnetic stator poles.
- **Hybrid Stepper Motor:** Combines principles of Permanent Magnet and Variable Reluctance motors for high precision and torque.
- **Winding Configurations:** Two-Phase and Three-Phase Stator Windings; Single-Pole vs. Dipole Pair configurations.

### Hardware Specifications: 28BYJ-48 (5V Stepper Motor)

| Parameter | Specification |
| :--- | :--- |
| **Model** | 28BYJ-48-5V |
| **Rated Voltage** | 5V DC |
| **Number of Phases** | 4 |
| **Speed Variation Ratio** | 1/64 |
| **Stride Angle** | $5.625^\circ / 64$ |
| **Frequency** | 100 Hz |
| **DC Resistance** | $50\,\Omega \pm 7\%$ (at $25^\circ\text{C}$) |
| **Idle In-Traction Frequency** | $> 600\text{ Hz}$ |
| **Idle Out-Traction Frequency** | $> 1000\text{ Hz}$ |
| **In-Traction Torque** | $> 34.3\text{ mN}\cdot\text{m}$ ($120\text{ Hz}$) |
| **Self-Positioning Torque** | $> 34.3\text{ mN}\cdot\text{m}$ |
| **Friction Torque** | $600 - 1200\text{ gf}\cdot\text{cm}$ |
| **Pull-in Torque** | $300\text{ gf}\cdot\text{cm}$ |
| **Insulation Resistance** | $> 10\text{ M}\Omega$ ($500\text{V}$) |
| **Insulated Electricity Power** | $600\text{ VAC} / 1\text{mA} / 1\text{s}$ |
| **Noise Level** | $< 35\text{ dB}$ ($120\text{ Hz}$, No load, $10\text{cm}$) |

---

## 🔌 Circuit Pin Mapping (Arduino to ULN2003 Driver)

The **28BYJ-48** stepper motor is driven using a **ULN2003 / ULN2003A** Darlington transistor array driver module.

```
+------------------+         +--------------------+         +-----------------------+
|  Arduino Board   |         | ULN2003 Driver IC  |         | 28BYJ-48 Stepper Motor|
+------------------+         +--------------------+         +-----------------------+
| Pin 8 (P8)  ------> IN1 -->| OUT1 (Pin 16) -------------> Blue (Coil 4)           |
| Pin 9 (P9)  ------> IN2 -->| OUT2 (Pin 15) -------------> Pink (Coil 3)           |
| Pin 10 (P10) -----> IN3 -->| OUT3 (Pin 14) -------------> Yellow (Coil 2)         |
| Pin 11 (P11) -----> IN4 -->| OUT4 (Pin 13) -------------> Orange (Coil 1)         |
| GND ---------------> GND -->| Pin 8 (GND)       |         |                       |
+------------------+         +--------------------+         |                       |
                               | COM (Pin 9)  -------------> Red (Common VCC)       |
                               | External +5V Power Supply -> Red (Common VCC)       |
                               +--------------------+---------+-----------------------+
```

---

## 🛠️ Lab Assignments

### Task 1: Basic Stepper Motor Interfacing
**Objective:** Interface an Arduino with the 28BYJ-48 stepper motor using the ULN2003 driver board and establish basic step/rotation control.

### Task 2: Smart Parking Barrier Gate (IR Sensor + Stepper Motor)
**Objective:** Connect an Infrared (IR) sensor to the system to act as a proximity trigger.
- **Behavior:** When an object/vehicle is detected by the IR sensor, rotate the motor $90^\circ$ to open the barrier gate.
- **Customization:** Adjust motor speed dynamically for gate opening and closing sequences.

### Task 3: Automatic Smart Curtain System (LDR Sensor + Stepper Motor)
**Objective:** Connect a Light Dependent Resistor (LDR) sensor to monitor ambient light levels.
- **Behavior:** Control the rotation angle and direction of the motor based on light intensity levels to simulate opening/closing curtains.
- **Customization:** Vary motor speed relative to light intensity changes.

Made by ❤️ [listening](https://www.youtube.com/watch?v=cvzu3bKgt5Y&list=RDcvzu3bKgt5Y&start_radio=1) to this and [this](https://www.youtube.com/watch?v=_KhsQ3nn6Kw&list=RD_KhsQ3nn6Kw&start_radio=1).
---
