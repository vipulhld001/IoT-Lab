This code uses the ESP32 with the API.
ThingSpeak service is used in this example, but people can use any other service to do so.
Please make sure you are using a network that allows ThingSpeak to access your network (Firewall Issues exist when people use University Networks).

# ESP32 & DHT11 Weather Station with ThingSpeak

An IoT-based environmental monitoring system that leverages an **ESP32** microcontroller and a **DHT11** sensor to measure temperature and relative humidity. Data is transmitted securely over Wi-Fi and visualised in real-time using the **ThingSpeak** cloud platform.

---


## System Architecture

```text
+-------------------+             Signal             +-------------------+
|   DHT11 Sensor    | -----------------------------> |   ESP32 Board     |
| (Temp & Humidity) |      (Data Pin: GPIO 27)       | (NodeMCU / DevKit)|
+-------------------+                                +-------------------+
                                                               |
                                                               | Wi-Fi Connection
                                                               v
                                                     +-------------------+
                                                     | ThingSpeak Cloud  |
                                                     |  Field 3: Temp    |
                                                     |  Field 4: Humid   |
                                                     +-------------------+
```
## Hardware Requirements & Wiring

### Components
* **ESP32 Development Board** (e.g., ESP32 WROOM 32D)
* **DHT11 Temperature & Humidity Sensor**
* **10kΩ Resistor** (If using a bare DHT11 sensor instead of a pre-assembled module with a built-in pull-up)
* Jumper wires and breadboard

### Pinout Configuration
| DHT11 Pin | Description | ESP32 Connection |
| :---: | :--- | :---: |
| **VCC** | Power Supply (3.3V - 5V) | **3V3** |
| **DATA** | Digital Signal Output | **GPIO 27** |
| **GND** | Ground | **GND** |

---

## Software & Setup Requirements

### 1. Arduino IDE Dependencies
Install the following libraries using the Library Manager (**Sketch** > **Include Library** > **Manage Libraries...**):
* **DHT sensor library** by Adafruit (and its prerequisite *Adafruit Unified Sensor* library)
* **ThingSpeak** by MathWorks

### 2. ThingSpeak Channel Configurations
1. Log into your [ThingSpeak Account](https://thingspeak.com/).
2. Create a **New Channel**.
3. Activate the following specific fields to match the code payload:
   * **Field 3:** Temperature (°C)
   * **Field 4:** Humidity (%)
4. Copy your **Channel ID** and **Write API Key** from the *API Keys* tab into the code variables (`myChannelNumber` and `myWriteAPIKey`).

---

## Firmware Configuration

The current code is pre-configured with the following network credentials. Update these variables if your router properties change:

```python
char* ssid = "Woah";             // Wi-Fi Access Point Name
char* passphrase = "idontknow?"; // Wi-Fi Password

unsigned long myChannelNumber = 1;      // Replace with your actual Channel ID
const char * myWriteAPIKey = "YOURKEY"; // Replace with your Write API Key
```
