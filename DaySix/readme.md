# IoT Lab 6: DHT Sensors & Temperature Measurement

**Presenter:** Vipul Singh Negi  
**Department:** Computer Science and Engineering, National Institute of Technology Rourkela  

---

## 📌 Problem Overview

> **Question:** *I want to find out the Room Temperature. What sensor should I choose?*

The solution presented in this lab is the **DHT (Digital Humidity and Temperature)** sensor module.

---

## 🌡️ Introduction to DHT Sensors

**DHT** stands for **Digital Humidity and Temperature**. It is a low-cost digital sensor designed for sensing temperature and humidity instantaneously.

### Key Characteristics:
- Easily interfaced with microcontrollers such as **Arduino** and **Raspberry Pi**.
- Provides calibrated digital signal output.
- Measures both relative humidity and ambient temperature.

---

## ⚖️ DHT11 vs. DHT22 Comparison

There are two primary versions of the DHT sensor series:

| Specification | DHT11 | DHT22 (AM2302) |
| :--- | :--- | :--- |
| **Humidity Range** | 20% to 80% RH | 0% to 100% RH |
| **Humidity Accuracy** | ±5% | ±2% |
| **Temperature Range** | 0°C to 50°C | -40°C to 80°C |
| **Temperature Accuracy** | ±2°C | ±0.5°C |
| **Physical Size** | Smaller | Larger |

---

## 🛠️ Internal Working Principle

Removing the outer casing of a DHT sensor reveals two primary sensing elements along with supporting circuitry:

1. **Humidity Sensing Element (Polymeric Membrane Capacitive/Resistive Sensor):**
   - Consists of two electrodes with a moisture-holding substrate (salt or conductive plastic polymer) on a glass substrate.
   - As ambient humidity increases, the substrate absorbs water vapor, releasing ions and decreasing resistance between the two electrodes.
   - The change in resistance is inversely proportional to relative humidity.

2. **Temperature Sensing Element (NTC Thermistor):**
   - Contains a **Negative Temperature Coefficient (NTC)** thermistor.
   - Unlike standard resistors, thermistor resistance changes dramatically with temperature changes (100+ $\Omega$/°C).
   - "Negative Coefficient" means electrical **resistance decreases as temperature increases**.

3. **Supporting Circuitry:**
   - Includes a $10	ext{ k}\Omega$ pull-up resistor and a decoupling capacitor on board.

---

## 📐 Mathematical Formulation (NTC Beta Constant)

The relation between temperature and resistance for the NTC thermistor is governed by the Beta equation:

$$B_{(T_1/T_2)} = rac{T_2 	\times T_1}{T_2 - T_1} 	\times \ln\left(rac{R_1}{R_2}
\right)$$

### Parameter Definitions:
- $B_{(T_1/T_2)}$: Beta Constant / material sensitivity parameter in Kelvin ($K$), typically between $3000	ext{ K}$ and $5000	ext{ K}$.
- $T_1$: Reference baseline temperature in Kelvin ($K$) (typically $25^\circ	ext{C} = 298.15	ext{ K}$).
- $T_2$: Target measured temperature in Kelvin ($K$).
- $R_1$: Electrical resistance at baseline temperature $T_1$ ($\Omega$).
- $R_2$: Electrical resistance at target temperature $T_2$ ($\Omega$).
- $\ln$: Natural logarithm function.

---

## 🔌 Circuit Pinout & Connection Guide

### Pin Mapping (DHT11 / DHT22 Module):
- **VCC ($+$):** Connect to **5V** or **3.3V** pin on Arduino Uno.
- **DATA ($S$ / Out):** Connect to a Digital I/O pin (e.g., **Digital Pin 2**) with a $10	ext{ k}\Omega$ pull-up resistor to VCC if using a bare 4-pin sensor.
- **GND ($-$):** Connect to Arduino **GND**.

---

<p align="center">
  <img src="[https://technobyte.org/wp-content/uploads/2019/09/CONEXION_DHT11-768x558.jpg]" alt="DHT 11 Connection" width="600"/>
</p>

<p align="center">
  <img src="https://cdn.shopify.com/s/files/1/0841/0673/9987/files/ldr-applications_480x480.webp" alt="Cadmium Sulfide CdS Breaking Bad Logo" width="600"/>
</p>

## 💻 Software Setup & Code

### Installing the Library in Arduino IDE:
1. Go to **Sketch** $
ightarrow$ **Include Library** $
ightarrow$ **Manage Libraries...**
2. Search for and install **`dhtlib`** or **`DHT sensor library` by Adafruit**.

---

### Internal ATmega328P Temperature Sensor Code (Bonus Code)

This code reads the internal temperature sensor built directly into the ATmega328P chip using the internal 1.1V ADC reference voltage:

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  Serial.println(readTemp(), DEC);
  delay(1000);
}

long readTemp() {
  long result; 
  // Read internal temperature sensor against 1.1V reference voltage
  ADMUX = _BV(REFS1) | _BV(REFS0) | _BV(MUX3); 
  delay(2); // Wait for Vref to settle
  
  ADCSRA |= _BV(ADSC); // Start AD conversion
  while (bit_is_set(ADCSRA, ADSC)); // Wait until conversion completes
  
  result = ADCL;
  result |= ADCH << 8;
  
  // Convert raw ADC value to temperature metric
  result = (result - 125) * 1075; 
  return result;
}
```

---

## 📝 Lab Assignments

Complete the following three tasks in your **Lab Record Books**:

1. **Assignment 1:** Interface the DHT sensor with Arduino to measure and output **Relative Humidity**.
2. **Assignment 2:** Interface the DHT sensor with Arduino to measure and output **Temperature in Celsius**.
3. **Assignment 3:** Extend the program to convert the measured Celsius temperature into **Fahrenheit** ($F = C 	imes rac{9}{5} + 32$).

### Submission Requirements:
- Draw circuit diagrams on the blank page of your Lab Record Book.
- Upload code as `.ino` files to Microsoft Teams.
- Include a header comment in each code file signed with your **Name** and **Roll Number**.
