# 🔥 Arduino Fire Alarm System

A multi-sensor fire detection and alert system built with Arduino as part of an **Electronic Devices and Circuits** course project. The system continuously monitors for flame, smoke, and abnormal temperature, triggering visual and audio alarms upon detecting any danger.

---

## 📋 Table of Contents

- [Features](#features)
- [Hardware Components](#hardware-components)
- [Circuit Connections](#circuit-connections)
- [How It Works](#how-it-works)
- [Thresholds & Configuration](#thresholds--configuration)
- [Getting Started](#getting-started)
- [Serial Monitor Output](#serial-monitor-output)
- [Project Structure](#project-structure)
- [Future Improvements](#future-improvements)

---

## ✨ Features

- 🔥 **Flame detection** via infrared flame sensor
- 💨 **Smoke detection** via MQ-series analog gas/smoke sensor
- 🌡️ **Temperature monitoring** via DHT11 sensor
- 📟 **16×2 I2C LCD** display for real-time status
- 🔴 Red LED alarm indicator & 🟢 Green LED safe indicator
- 🔊 Buzzer alarm on danger detection
- 📡 Serial monitor logging for debugging

---

## 🧰 Hardware Components

| Component | Description |
|---|---|
| Arduino Uno/Nano | Microcontroller |
| DHT11 | Temperature & Humidity Sensor |
| Flame Sensor | IR-based flame detector (digital output) |
| MQ-2 / MQ-135 | Smoke / Gas Sensor (analog output) |
| 16×2 LCD (I2C) | Display module (address `0x27`) |
| Buzzer | Piezo buzzer for audio alert |
| Red LED | Danger indicator |
| Green LED | Safe/normal indicator |
| Resistors | Current limiting for LEDs |
| Breadboard & Wires | For prototyping |

---

## 🔌 Circuit Connections

| Component | Arduino Pin |
|---|---|
| Flame Sensor (OUT) | Digital Pin **2** |
| DHT11 (DATA) | Digital Pin **3** |
| Buzzer | Digital Pin **4** |
| Red LED | Digital Pin **5** |
| Green LED | Digital Pin **6** |
| Smoke Sensor (AOUT) | Analog Pin **A0** |
| LCD SDA | **A4** (SDA) |
| LCD SCL | **A5** (SCL) |

> ⚠️ Connect all VCC pins to 5V and all GND pins to Arduino GND.

---

## ⚙️ How It Works

The system runs a continuous loop checking three independent sensors:

1. **Flame Sensor** — Reads a digital `LOW` signal when flame/fire is detected (active LOW).
2. **Smoke Sensor** — Reads an analog value from A0; values above the threshold indicate smoke.
3. **DHT11** — Reads ambient temperature; values above the threshold indicate abnormal heat.

**If any sensor triggers:**
- Buzzer turns ON
- Red LED turns ON, Green LED turns OFF
- LCD displays `!!! FIRE ALERT !!!` with the specific cause

**If all sensors are safe:**
- Buzzer and Red LED remain OFF
- Green LED stays ON
- LCD displays `System Normal` and the current temperature

---

## 🎛️ Thresholds & Configuration

You can adjust these `#define` values in the sketch to calibrate for your environment:

```cpp
#define SMOKE_THRESHOLD  300   // Analog value (0–1023) above which smoke is detected
#define TEMP_THRESHOLD   50    // Temperature in °C above which high-heat alert triggers
```

> 💡 **Tip:** Run the system in a normal environment first and observe the smoke sensor's baseline reading via Serial Monitor. Set `SMOKE_THRESHOLD` slightly above that baseline.

---

## 🚀 Getting Started

### Prerequisites

- [Arduino IDE](https://www.arduino.cc/en/software)
- The following libraries (install via Library Manager):
  - `DHT sensor library` by Adafruit
  - `LiquidCrystal_I2C` by Frank de Brabander
  - `Wire` (built-in)

### Steps

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/fire-alarm-system.git
   ```
2. Open `fire_alarm.ino` in the Arduino IDE.
3. Install required libraries via **Sketch → Include Library → Manage Libraries**.
4. Select your board and COM port under **Tools**.
5. Upload the sketch.
6. Open Serial Monitor at **9600 baud** to view live sensor readings.

---

## 📡 Serial Monitor Output

```
Flame: 1 | Smoke: 142 | Temp: 28.00
Flame: 1 | Smoke: 145 | Temp: 28.00
Flame: 0 | Smoke: 148 | Temp: 29.00   ← Flame detected!
```

---

## 📁 Project Structure

```
fire-alarm-system/
├── fire_alarm.ino       # Main Arduino sketch
└── README.md            # Project documentation
```

---

## 🔮 Future Improvements

- [ ] Add GSM module to send SMS alerts
- [ ] Integrate Wi-Fi (ESP8266/ESP32) for IoT-based notifications
- [ ] Add a reset button to silence the alarm manually
- [ ] Log sensor data to an SD card for historical analysis
- [ ] Use MQ-2 with proper calibration curve for accurate PPM readings

---

## 📚 Course

**Electronic Devices and Circuits** — Undergraduate Engineering Project

---

## 📄 License

This project is open-source and available under the [APACHE 2.0 License](LICENSE).
