# IoT Lab 9: ESP32 Microcontroller & Wireless Communication

This repository contains technical notes, hardware pinouts, architectural specifications, setup guides, and practical lab assignments for **IoT Lab 9**.

## 📋 Course Information

* **Course:** Internet of Things (IoT) Lab
* **Instructor:** Vipul Singh Negi

---

## 📑 Overview: What is ESP32?

The **ESP32** is a low-cost, low-power **System on a Chip (SoC)** microcontroller series engineered by **Espressif Systems** as the successor to the popular ESP8266. It features integrated **2.4 GHz Wi-Fi** and **dual-mode Bluetooth (Classic and BLE)**.

### Key Capabilities
* Built-in antenna switches, RF balun, power amplifier, low-noise receive amplifier, and power management modules.
* Designed for mobile devices, wearable electronics, and smart IoT edge applications.
* Ultra-low power modes with dedicated ULP (Ultra Low Power) co-processor.
* Native support for MicroPython, FreeRTOS, and Arduino framework.

---

## ⚙️ Specifications & Features

| Specification | Details |
| :--- | :--- |
| **CPU Cores** | Dual-core (or single-core in ESP32-S0WD) |
| **Architecture** | 32-bit Tensilica Xtensa LX6 |
| **Clock Frequency** | Up to 240 MHz (Performance up to 600 DMIPS) |
| **Internal ROM** | 448 KB (Booting and core functions) |
| **Internal SRAM** | 520 KB |
| **RTC SRAM** | 16 KB (8 KB Fast SRAM + 8 KB Slow SRAM for sleep modes) |
| **eFuse** | 1024 bits (256 bits system/MAC, 768 bits user app reserved) |
| **External Memory** | Up to $4 \times 16\text{ MB}$ QSPI Flash & SRAM with hardware AES encryption |
| **Wi-Fi** | IEEE 802.11 b/g/n (Up to 150 Mbps) |
| **Bluetooth** | Bluetooth v4.2 BR/EDR and BLE (Bluetooth Low Energy) |
| **GPIO Count** | 36 physical GPIOs (Multiple multiplexed functions) |
| **ADC / DAC** | 18 Channels 12-bit ADC / 2 Channels 8-bit DAC |
| **Peripheral Interfaces**| SPI, $I^2C$, UART, $I^2S$, CAN (TWAI®), PWM, Touch Sensors |

---

## 📐 Pinout & Boot Flow Diagram

### Important GPIO Pin Categories

* **Input-Only Pins:** GPIO 34, 35, 36 (VP), 39 (VN) — No internal pull-up/pull-down resistors.
* **SPI Flash Reserved Pins:** GPIO 6 to GPIO 11 are connected to internal SPI Flash. **Do not use for general I/O.**
* **Touch Pins:** GPIO 0, 2, 4, 12, 13, 14, 15, 27, 32, 33 (10 capacitive touch sensors).
* **ADC Channels:** ADC1 (GPIO 32–39), ADC2 (GPIO 0, 2, 4, 12–15, 25–27).

### Chip Boot Flow Logic

```
                    +-------------------+
                    |    Chip Reset     |
                    +---------+---------+
                              |
                     [Check Reset Cause]
                              |
            +-----------------+-----------------+
            |                                   |
     (Normal Reset)                     (Deep-Sleep Reset)
            |                                   |
    [Check Strapping]                   Jump to RTC Memory
      GPIO0, GPIO2                         Address
            |
      +-----+-----+
      |           |
   GPIO0=1     GPIO0=0
   GPIO2=x     GPIO2=0
      |           |
  Initialization Initialization
      |           |
Copy Flash->RAM  Wait for download
      |          via UART / SDIO
Jump to Entry
```

---

## 🛠️ Environment Setup Instructions

### 1. Arduino IDE ESP32 Board Manager Setup

1. Open **Arduino IDE** and go to **File $\rightarrow$ Preferences**.
2. Add the following URL into **Additional Boards Manager URLs**:
   ```url
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
3. Go to **Tools $\rightarrow$ Board $\rightarrow$ Boards Manager...**
4. Search for `esp32` and click **Install** on **ESP32 by Espressif Systems**.

### 2. USB to UART Drivers
If your system does not detect the ESP32 COM port, download and install the **CP210x Drivers** from Silicon Labs:
* [CP210x VCP Drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

---

## 💻 Code Examples

### 1. Simple On-Board LED Blink Test

```cpp
#define LED_PIN 2

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(50);
  digitalWrite(LED_PIN, LOW);
  delay(50);
}
```

### 2. Scanning Available Wi-Fi Networks
Check Ezamples

### 3. ESP32 Bluetooth Serial Communication (Slave Mode)
Check Examples

## 📱 Mobile App Setup for Bluetooth Testing

1. Download **Serial Bluetooth Terminal** from the Google Play Store / App Store.
2. Open Bluetooth settings on your smartphone and pair with `ESP32-BT-Slave`.
3. Open the **Serial Bluetooth Terminal** app, navigate to **Devices**, and select `ESP32-BT-Slave` to connect.

---

## 🧪 Lab Assignments

### Assignment 1: Full RGB LED Control with ESP32
**Objective:** Write an Arduino C++ program to interface a common cathode/anode RGB LED with the ESP32. Cycle through all primary and secondary colors (Red, Green, Blue, Yellow, Cyan, Magenta, White) using PWM signals (`ledcWrite`).

### Assignment 2: Bluetooth Controlled RGB LED Lighting System
**Objective:** Control the RGB LED colors wirelessly via a mobile phone using Bluetooth Serial communication.

* **Requirement:** 
  * Receiving character `'r'` or `'R'` $\rightarrow$ Set color to **Red**.
  * Receiving character `'g'` or `'G'` $\rightarrow$ Set color to **Green**.
  * Receiving character `'b'` or `'b'` $\rightarrow$ Set color to **Blue**.
  * Support custom commands for off/white states or color mixing.
 

Music that goes best with this:

1. Knife Party - [Bonfire](https://youtu.be/e-IWRmpefzE)
2. The Chemical Brothers - [Galvanize](https://www.youtube.com/watch?v=Xu3FTEmN-eg&list=RDXu3FTEmN-eg&start_radio=1)
