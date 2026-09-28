# Internet of Things - Lab 7: Sensors Interfacing

**Author:** Vipul Singh Negi  


---

## Table of Contents
1. [Overview](#overview)
2. [Temperature Sensor Module](#temperature-sensor-module)
   - [Introduction & Classification](#introduction--classification)
   - [NTC Thermistor & Module Components](#ntc-thermistor--module-components)
   - [Working Principle & Circuit Diagrams](#working-principle--circuit-diagrams)
   - [Code Example: Interfacing Analog Temperature Sensor](#code-example-interfacing-analog-temperature-sensor)
3. [Soil Moisture Sensor Module](#soil-moisture-sensor-module)
   - [Introduction & Volumetric Water Content](#introduction--volumetric-water-content)
   - [Water Content Formula & Soil Composition](#water-content-formula--soil-composition)
   - [Pin Configuration & Specifications](#pin-configuration--specifications)
   - [Working Principle](#working-principle)
4. [Lab Assignments](#lab-assignments)

---

## Overview
This laboratory session covers interfacing techniques for two common analog/digital IoT sensors:
1. **Analog Temperature Sensor Module** (using an NTC thermistor and an LM393 comparator).
2. **Soil Moisture Sensor Module** (measuring soil volumetric water content via resistance/dielectric properties).

---

## Temperature Sensor Module

### Introduction & Classification
* **Analog Temperature Sensors:** Provide current or voltage output proportional to absolute temperature, achieving accuracies up to $\pm 1^\circ\text{C}$.
* **Definition:** A component that senses temperature and converts thermal variations into measurable electrical signals.
* **Classification:**
  * **Thermal Resistors (Thermistors)**
  * **Thermocouples**

### NTC Thermistor & Module Components
* **Thermistor Characteristics:** Made of semiconductor materials. Most standard modules utilize **Negative Temperature Coefficient (NTC)** thermistors, where resistance **decreases** as temperature **increases**.
* **Sensitivity:** Due to acute resistance changes relative to temperature variations, thermistors are among the most sensitive temperature-sensing elements.
* **LM393 Comparator Integration:** The sensor module includes an **LM393 dual-differential comparator IC**, allowing dual output:
  * **Analog Output ($A_0$):** Direct voltage output relative to thermistor resistance.
  * **Digital Output ($D_0$):** High/Low logic output determined by an adjustable onboard potentiometer threshold.

### Working Principle & Circuit Diagrams
1. **Threshold Adjustment:** The onboard potentiometer sets a reference threshold voltage for the LM393 comparator.
2. **Behavior:**
   * Touching or applying heat to the thermistor causes its resistance to drop, lowering the voltage on $A_0$.
   * When $A_0$ falls below the set reference threshold, $D_0$ toggles to a **HIGH** state.
   * Concurrently, the module's onboard indicator LED and an attached micro-controller LED (e.g., Pin 13 on Arduino Uno) turn off.
3. **Monitoring:** Both $A_0$ (raw analog values) and $D_0$ (digital switching states) can be monitored simultaneously via the Serial Monitor.

#### Schematic Overview
* **LM393 Connections:**
  * Pin 1: `1OUT` ($D_0$)
  * Pin 2: `1IN-` ($A_0$)
  * Pin 3: `1IN+` (Potentiometer Threshold)
  * Pin 4: `GND`
  * Pin 8: `VCC`
* **Header Pins:** `1: D0`, `2: A0`, `3: VCC`, `4: GND`

---

### Code Example: Interfacing Analog Temperature Sensor

The following Arduino C++ snippet reads analog values from pin `A0` and applies the **Steinhart-Hart / Beta equation** to convert the raw reading into degrees Celsius ($^\circ\text{C}$).

```cpp
const float BETA = 3950; // Should match the Beta Coefficient of the thermistor

void setup() {
  Serial.begin(9600);
}

void loop() {
  int analogValue = analogRead(A0);
  
  // Calculate temperature in Celsius using the Beta parameter formula
  float celsius = 1.0 / (log(1.0 / (1023.0 / analogValue - 1.0)) / BETA + 1.0 / 298.15) - 273.15;
  
  Serial.print("Temperature: ");
  Serial.print(celsius);
  Serial.println(" °C");
  
  delay(1000);
}
```

---

## Soil Moisture Sensor Module

### Introduction & Volumetric Water Content
* **Purpose:** Measures the volumetric water content (VWC) within soil.
* **Indirect Measurement:** Direct gravimetric measurement requires soil sampling, drying, and weighing. Soil moisture sensors estimate moisture indirectly by assessing properties such as electrical resistance, dielectric constant, or neutron interactions.
* **Calibration Factors:** Environmental parameters—including soil type, temperature, and electrical conductivity—can affect readings and require calibration.
* **Applications:** Widely used in automated agricultural irrigation, remote sensing, and hydrological monitoring.
* **Water Potential Sensors:** Advanced variants (e.g., gypsum blocks, tensiometers) calculate soil water potential rather than purely volumetric content.

<p align="center">
  <img src="https://europe1.discourse-cdn.com/arduino/optimized/4X/3/7/1/371d2a082793927e2574b5d2cfde7aa1e07ddb1e_2_750x750.jpeg" alt="Soil Moisture Sensor" width="600"/>
</p>


### Water Content Formula & Soil Composition

#### Volumetric Water Content (VWC) Formula
$$\theta = \frac{V_W}{V_T}$$

Where:
* $\theta$ = Volumetric Water Content (VWC)
* $V_W$ = Volume of Water
* $V_T$ = Total Sample Volume

#### Example Soil Phase Compositions (Volume Distribution)
| Soil Condition | Soil Minerals | Pore Water | Air Space |
| :--- | :--- | :--- | :--- |
| **Saturated / Wet Soil** | 55% | 42% | 3% |
| **Moist Soil** | 55% | 10% | 35% |
| **Dry Soil** | 55% | 1% | 44% |

---

### Pin Configuration & Specifications

#### Pinout
* **VCC:** Power Supply Input ($5\text{V}$)
* **GND:** Ground Reference
* **A0:** Analog Output signal
* **D0:** Digital Output signal (via LM393 comparator threshold)

#### Technical Specifications
* **Operating Voltage:** $5\text{V DC}$
* **Operating Current:** $< 20\text{mA}$
* **Interface Type:** Analog & Digital
* **Operating Temperature:** $10^\circ\text{C} \sim 30^\circ\text{C}$

---

### Working Principle
1. Soil moisture is critical for root development and nutrient absorption.
2. Water helps regulate plant temperature through process like transpiration.
3. Excessive moisture levels lead to anaerobic soil conditions, encouraging pathogens and harming plant growth.
4. The probe measures electrical conductivity between two exposed pads inserted into the soil. Higher water content increases conductivity (lowers resistance), altering the output voltage at $A_0$. The onboard LM393 comparator compares $A_0$ against a preset threshold on the potentiometer to switch $D_0$ HIGH/LOW.

---

## Lab Assignments

1. **Assignment 1:** Write an Arduino program (WAP) to interface with the Soil Moisture Sensor and read basic moisture data.
2. **Assignment 2:** Write an Arduino program (WAP) to read and display both the **Analog** ($A_0$) and **Digital** ($D_0$) outputs of the Soil Moisture Sensor.
3. **Assignment 3:** Write an Arduino program (WAP) to divide the soil moisture readings into **5 distinct range categories** (e.g., *Very Dry, Dry, Moderate, Wet, Saturated*).
4. **Assignment 4:** Write an Arduino program (WAP) to map the 5 soil moisture ranges to **5 different LED colors** (or an RGB LED) to visually indicate moisture levels.

---

Made by ❤️ [listening](https://www.youtube.com/watch?v=cvzu3bKgt5Y&list=RDcvzu3bKgt5Y&start_radio=1) to this and [this](https://www.youtube.com/watch?v=_KhsQ3nn6Kw&list=RD_KhsQ3nn6Kw&start_radio=1).

