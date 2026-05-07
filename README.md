# ESP8266 Motion-Aware Smartwatch Prototype

**Embedded wearable firmware for an ESP8266-based smartwatch prototype with OLED display, RTC timekeeping, MPU-6050 motion sensing, LiPo power monitoring, button navigation, buzzer feedback, and motion-aware display behavior.**

This project demonstrates a complete embedded firmware prototype for a custom ESP8266 wearable device. It integrates multiple I2C peripherals, real-time sensor sampling, display rendering, physical input handling, power-related UI behavior, and a small multi-screen user interface suitable for a proof-of-concept smartwatch or wearable controller.

The goal of this project is not just to show an Arduino sketch running on an ESP8266. It shows the kind of practical firmware engineering required to bring together hardware modules, sensor data, user interaction, display constraints, timing behavior, and device-state logic into one working embedded product prototype.

![Screenshot 2025-05-20 at 05 35 09](https://github.com/user-attachments/assets/7feb14fe-da48-4b06-a518-bcba1308e57b)
![Screenshot 2025-05-22 at 06 16 47](https://github.com/user-attachments/assets/787b6f50-537a-4345-809e-63239274b4c9)

---

## Why This Project Matters

This repository highlights hands-on embedded and firmware engineering experience in several areas that are valuable in real-world connected-device development:

- Multi-peripheral firmware integration over I2C
- OLED display rendering on a constrained embedded device
- Real-time clock integration and time/date formatting
- Motion sensing with accelerometer and gyroscope data
- Motion-aware UI behavior and display power/brightness control
- Physical button input handling
- Buzzer/haptic-style user feedback
- Battery-monitoring hardware integration
- Wearable-device product thinking
- Debugging hardware address conflicts on shared buses
- Building firmware around real hardware constraints instead of simulator-only logic

---

## Project Overview

**Watch Me** is an ESP8266-based smartwatch prototype. The firmware drives a small OLED display, reads real-time clock data, samples motion data from an MPU-6050 accelerometer/gyroscope, responds to a hardware button, provides buzzer feedback, and changes display behavior based on inactivity/movement detection.

The prototype includes multiple screens, including:

- Main clock screen
- Date and day-of-week display
- Accelerometer data screen
- Gyroscope data screen
- Temperature screen from the MPU-6050
- Battery-level screen concept
- Time-adjustment screens
- Early concept screen for a motion-based “Heads Up” game mode

---

## Hardware Used

The project was designed around the following embedded hardware modules:

| Component | Purpose |
|---|---|
| ESP8266 | Main microcontroller and firmware target |
| 0.98" OLED Display | I2C display for watch UI |
| RTC DS1307 / DS3231-style RTC module | Real-time clock source |
| MPU-6050 / GY-521 | Accelerometer, gyroscope, and temperature sensing |
| LC709203F Fuel Gauge | LiPo battery-level monitoring |
| 3.7V LiPo Battery | Portable wearable power source |
| LiPo Charger | Battery charging support |
| 3V-to-5V Step-Up Converter | Power regulation for 5V modules |
| 3V Buzzer | Audible feedback |
| Tactile Buttons | User input and screen navigation |

---

## Firmware Features

### OLED User Interface

The firmware renders multiple screens on a 128x64 SSD1306 OLED display.

Implemented display modes include:

1. Clock
2. Acceleration
3. Gyroscope
4. Temperature

The UI is intentionally simple and readable for a small wearable display. It uses clear text layouts, compact sensor readouts, and screen switching through hardware input.

---

### Real-Time Clock Integration

The firmware reads date and time data from an RTC module and formats it for display.

Supported clock information includes:

- Hour
- Minute
- Second
- AM/PM indicator
- Month
- Day
- Year
- Day of week

The RTC logic allows the watch to keep time independently of the ESP8266 runtime state.

---

### Motion Sensing

The firmware initializes and reads data from an MPU-6050 motion sensor.

Sensor data includes:

- Acceleration X/Y/Z
- Gyroscope X/Y/Z
- Temperature

The accelerometer and gyroscope data are used both for display purposes and for detecting whether the device is moving or inactive.

---

### Motion-Aware Display Behavior

A key feature of the prototype is activity-aware display behavior.

The firmware compares motion readings over time. If the device appears inactive for a defined timeout period, the OLED contrast is reduced. When movement is detected again, the display returns to a higher visibility state.

This demonstrates a practical wearable-device concept: balancing user visibility with power-conscious behavior.

---

### Button-Based Navigation

A hardware button is used to cycle between display modes.

The firmware monitors button state changes and advances the UI to the next screen when the button is pressed. This creates a simple wearable-style navigation model without needing a touchscreen.

---

### Buzzer Feedback

The firmware includes buzzer support for simple audible feedback. This can be used for startup confirmation, button feedback, alerts, or future interaction states.

---

### Battery Monitoring Concept

The hardware design includes an LC709203F LiPo / Li-Ion fuel gauge. The README in the original project notes that battery-level reading was tested successfully, even though some photos were captured without a battery connected.

This demonstrates awareness of portable-device power monitoring, which is an important part of wearable and IoT firmware development.

---

## Embedded Engineering Highlights

This project demonstrates several practical firmware skills:

### Shared I2C Bus Management

The project uses multiple I2C devices on the same bus, including the OLED, RTC, fuel gauge, and MPU-6050. The code accounts for I2C address conflicts by using the MPU-6050 alternate address behavior through the AD0 pin.

### Hardware Bring-Up

The firmware includes initialization checks for core peripherals, including the display, RTC, and motion sensor. This is typical of hardware bring-up workflows where each peripheral must be confirmed before higher-level behavior is reliable.

### Sensor Configuration

The MPU-6050 is configured with defined accelerometer range, gyroscope range, and filter bandwidth settings. This shows practical sensor setup beyond simply reading default values.

### Product-Oriented Firmware

The firmware is written around a physical user experience: clock display, screen navigation, motion-triggered display changes, feedback, and battery-awareness. That makes this more than a board test; it is a wearable product prototype.

---

## Skills Demonstrated

- C++ / Arduino firmware development
- ESP8266 embedded development
- I2C peripheral integration
- OLED display control with Adafruit SSD1306 / GFX
- RTC integration with RTClib
- MPU-6050 accelerometer and gyroscope integration
- Embedded input handling
- Display state management
- Motion-based interaction logic
- Battery-monitoring hardware integration
- Wearable-device prototyping
- Hardware/software debugging
- Embedded product design thinking

---

## Repository Structure

```text
esp8266_watch_me/
├── README.md
├── LICENSE
└── watch_me/
    ├── watch_me.ino
    ├── heads_up.jpg
    └── heads_up_logo.jpg
```

---

## Main Firmware File

The main firmware is located at:

```text
watch_me/watch_me.ino
```

This file contains:

- Peripheral initialization
- Main firmware loop
- OLED display rendering
- RTC read/format logic
- MPU-6050 sensor reading
- Button input handling
- Motion/inactivity detection
- Contrast control
- Buzzer feedback

---

## Suggested GitHub Repository Title

**ESP8266 Motion-Aware Smartwatch Prototype with OLED, RTC, MPU-6050, and LiPo Monitoring**

---

## Suggested GitHub Repository Description

ESP8266 smartwatch firmware prototype with OLED UI, RTC timekeeping, MPU-6050 motion sensing, LiPo battery monitoring, button navigation, buzzer feedback, and motion-aware display behavior.

---

## Future Improvements

Possible next improvements include:

- Add a schematic and wiring diagram
- Add photos of the final assembled prototype
- Document exact pin mappings
- Add a battery screen implementation section
- Add RTC time-setting workflow documentation
- Improve button debouncing
- Add low-power sleep modes
- Add Wi-Fi sync or OTA update support
- Complete the motion-based Heads Up game mode
- Split firmware into multiple source files for maintainability
- Add serial debug command controls for firmware testing

---

## About This Project

This project is part of a hands-on embedded systems portfolio focused on building real hardware prototypes, integrating sensors and peripherals, and writing firmware that supports practical product behavior.

It is especially relevant for roles involving:

- Embedded Software Engineering
- Firmware Engineering
- IoT Device Development
- Wearable Device Prototyping
- Hardware/Firmware Integration
- Sensor-Based Product Development

---

## <ins>**The functionality includes the following:**</ins>

#### * The first screen displays the main clock at rest, with the format hh:mm AM/PM
![PXL_20250519_205457624](https://github.com/user-attachments/assets/547338b1-fd94-47e9-895d-2206eb1b5d64)

#### 1) When the watch is first at rest, and not moving at all, the LED brightness level is very high;

#### 2) After a second, the LED brightness is set to low;

#### 3) When the watch is moved again, the LED brightness is set to high again;

#### 4) If the movement is enough, the clock screen changes to;
![PXL_20250519_205509609](https://github.com/user-attachments/assets/ef00a01f-e5ee-470d-8d53-a4184bebf713)

![PXL_20250519_205509165 MP](https://github.com/user-attachments/assets/e05f4207-6014-46f0-b6e2-5c1a2d730aec)

#### 5) If you press the button for the D5 pin, then you go to the next screen;
![PXL_20250519_223457380](https://github.com/user-attachments/assets/a2fc9f93-6531-4b29-b156-0d8570587295)

#### 6) The next screen reads the Gyroscope data and displays it;
![PXL_20250519_205207516](https://github.com/user-attachments/assets/45949adf-0ae0-4907-905c-121cdd459b27)

#### 7) The next screen reads the Accelerometer data and displays it;
![PXL_20250519_205219659 MP](https://github.com/user-attachments/assets/f8f9058f-9e96-4483-9f15-b9145c98ba36)

#### 8) The next screen is the beginning of a game of "Heads Up". I have not yet implemented the logic, however the plan is for the user to hold the device to their forehead and quickly flip forward or backwards, which will increase or decrease points, at the same time as the screen displays the next word the the user needs to guess;
![PXL_20250519_205229828 MP](https://github.com/user-attachments/assets/d0eb8033-2162-4a3f-91cf-828a2a40183f)

#### 9) The next screen reads the battery level and displays it, however I don't have a battery hooked up in the picture, but I did test it and it works great;
![PXL_20250519_205242337](https://github.com/user-attachments/assets/1903e8b8-567b-45db-a474-4b8f514f6c41)
![4712-07](https://github.com/user-attachments/assets/beb255c2-de77-439e-a3da-afe7802c3de3)

#### 10) The next screen allows you to increase the hour by pressing the button for the D7 pin, which writes to the real time clock RTC (DS3231) and the time is maintained by a CR2032 coin cell;
![PXL_20250519_205333220](https://github.com/user-attachments/assets/ad816934-e790-4ec4-a7a3-843cf2bffd00)

#### 11) The next screen allows you to increase the minutes by pressing the button for the D7 pin, which writes to the real time clock RTC (DS3231) and the time is maintained by a CR2032 coin cell;
![PXL_20250519_205339630](https://github.com/user-attachments/assets/f684ecac-cf03-46cc-b72b-4ad7dc97df29)



## License

This repository uses the GPL-3.0 license.
