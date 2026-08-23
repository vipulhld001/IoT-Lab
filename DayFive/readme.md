# 💡 IoT Lab 5: Light Dependent Resistor (LDR) Interfacing & Control

**Author**: Vipul Singh Negi  
**Department**: Computer Science Engineering, National Institute of Technology Rourkela  
**Date**: August 23, 2026  

---

## 📌 Problem Statement
> *"How bright is this room? What sensor should we choose to measure light intensity?"*

To measure light intensity in an ambient environment, we use a **Light Dependent Resistor (LDR)**, a passive electronic component that alters its electrical resistance based on exposed light intensity.

---

## ⚛️ What is an LDR Sensor?
An **LDR (Light Dependent Resistor)** or photoresistor relies on the principle of **photoconductivity**:
* **In Darkness**: High resistance (typically up to several megaohms $\text{M}\Omega$).
* **Under Light**: Low resistance (drops to a few hundred ohms $\Omega$).

### 🔬 Components & Internal Structure
- **Semiconductor Material**: Cadmium Sulfide ($\text{CdS}$) deposited on a ceramic base.
- **Zig-Zag Pattern**: Designed to maximize surface area and light sensitivity.
- **Electrodes**: Two metallic contacts providing terminal connections.
- **Protective Layer**: Transparent glass/plastic cover protecting the photosensitive element.

<p align="center">
  <img src="watermarked_img_11353785204385914901.png" alt="Cadmium Sulfide CdS Breaking Bad Logo" width="600"/>
</p>

| Element | Symbol | Atomic Number | Role in LDR |
| :--- | :---: | :---: | :--- |
| **Cadmium** | **`Cd`** | **`48`** | Heavy metal cation forming semiconductor lattice |
| **Sulfur** | **`S`** | **`16`** | Chalcogen anion forming $\text{CdS}$ photoconductive layer |

---

## 🔌 Arduino Pin Modes Summary

| Mode | Behavior / Function |
| :--- | :--- |
| **`OUTPUT`** | Drives digital signals to actuators (e.g., turning an LED `HIGH` or `LOW`). |
| **`INPUT`** | Reads digital signals (`HIGH`/`LOW`) from external circuits or floating pins. |
| **`INPUT_PULLUP`** | Activates an internal microcontroller pull-up resistor ($20\text{k}\Omega - 50\text{k}\Omega$) to keep input `HIGH` by default when floating. |

---

## 💻 Lab Assignments & Solutions

### Assignment 1: Basic LDR Reading via Serial
Read continuous analog voltage values from the LDR sensor and print to Serial Monitor.



---

### Assignment 2: Threshold-Based Automatic Light Control
Turn an LED ON or OFF based on ambient light threshold (e.g., automatic street light system).



---

### Assignment 3: Proportional Dimming Control (PWM)
Dynamically adjust LED brightness using PWM (`analogWrite`), remapping the 10-bit analog input ($0 - 1023$) to an 8-bit output byte ($0 - 255$).


---

## 📜 References
- National Institute of Technology Rourkela — Department of Computer Science & Engineering
- IoT Lab Lecture 5: LDR Sensors & Actuator Interfacing
