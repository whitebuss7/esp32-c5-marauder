# Marauder C5 v2

**An ESP32-C5-based wireless network analysis and monitoring tool featuring a TFT touchscreen interface, Wi-Fi scanning, BLE discovery, NRF24L01 spectrum monitoring, and deauthentication detection.**

![Platform](https://img.shields.io/badge/Platform-ESP32--C5-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-00599C)
![Framework](https://img.shields.io/badge/Framework-Arduino-00979D)
![Version](https://img.shields.io/badge/Version-2.0-purple)
![License](https://img.shields.io/badge/License-MIT-green)

---

## Overview

Marauder C5 is an experimental wireless monitoring and analysis project built around the ESP32-C5 microcontroller. It combines Wi-Fi network discovery, Bluetooth Low Energy (BLE) scanning, NRF24L01 radio monitoring, and wireless management-frame detection in a touchscreen-controlled interface.

The project is designed for educational purposes, embedded systems development, and authorized wireless testing in controlled environments.

## Features

### Wi-Fi Tools

* **Wi-Fi Scanner** — Detect nearby Wi-Fi networks and display their SSIDs, signal strength (RSSI), and channels.
* **Channel Details** — View the number of detected networks on each supported 2.4 GHz channel.
* **Channel Analyzer** — Visualize channel occupancy using a graphical interface.
* **Beacon Transmission Experiment** — Experimental Wi-Fi beacon-frame transmission functionality. Hardware and firmware support may vary.

### Bluetooth Low Energy

* **BLE Scanner** — Discover nearby BLE advertisers and display device addresses, names, and RSSI values.
* **BLE Advertising Experiment** — Test BLE advertising payloads using predefined example data. Device compatibility and advertising behavior depend on the NimBLE stack and ESP32-C5 support.

### NRF24L01 Tools

* **Spectrum Monitor** — Sample radio activity across NRF24L01 channel settings and visualize the results.
* **Packet Counter** — Count packets received by the NRF24L01 on a selected channel.

> The NRF24L01 operates in the 2.4 GHz ISM band. Its channel activity readings are approximate and should not be interpreted as a calibrated RF spectrum measurement.

### Security Monitoring

* **Deauthentication Detection** — Monitor Wi-Fi management frames for deauthentication and disassociation events on a selected channel.
* **Event Logger** — Store recent diagnostic and monitoring events in a circular log buffer.
* **Hardware Status** — Display the chip model, CPU frequency, free heap, flash capacity, and peripheral initialization status.

### Touchscreen Interface

* ILI9341 TFT display
* XPT2046 resistive touchscreen
* Twelve-button main menu
* Dedicated back button on supported screens
* Color-coded status indicators
* Live counters and graphical channel visualization

## Hardware Requirements

| Component                      | Purpose                   |
| ------------------------------ | ------------------------- |
| ESP32-C5 development board     | Main microcontroller      |
| NRF24L01 module                | 2.4 GHz radio experiments |
| ILI9341 TFT display            | Graphical user interface  |
| XPT2046 touchscreen controller | Touch input               |
| Jumper wires                   | Connections               |
| Breadboard (optional)          | Prototyping               |

**Important:** Verify the voltage requirements and GPIO capabilities of your specific ESP32-C5 board before wiring the peripherals. Use appropriate logic-level compatibility and a suitable power supply.

## Pin Configuration

The following pin assignments are defined in the source code.

| Signal              | ESP32-C5 GPIO |
| ------------------- | ------------: |
| SPI SCK             |            23 |
| SPI MISO            |            25 |
| SPI MOSI            |            24 |
| TFT CS              |             4 |
| TFT DC              |             2 |
| TFT RST             |             3 |
| TFT LED / Backlight |             5 |
| Touch CS            |             6 |
| NRF24L01 CE         |             9 |
| NRF24L01 CSN        |            10 |

The TFT, touchscreen, and NRF24L01 share the SPI bus, using separate chip-select signals.

**GPIO compatibility note:** Confirm that these GPIO numbers are exposed and usable on your exact ESP32-C5 board. Some development boards use different pin mappings or reserve pins for onboard hardware.

## Software Requirements

* Arduino IDE
* ESP32 board support package compatible with your ESP32-C5 board
* A compatible version of the NimBLE-Arduino library
* The libraries listed below

### Required Libraries

Install these libraries through the Arduino IDE Library Manager where available:

* `Adafruit GFX Library`
* `Adafruit ILI9341`
* `XPT2046_Touchscreen`
* `RF24` by TMRh20
* `NimBLE-Arduino`
* ESP32 Arduino core libraries (`WiFi`, `SPI`, and ESP-IDF Wi-Fi APIs)

FreeRTOS synchronization and ESP32 system APIs are supplied by the ESP32 development framework.

## Installation

1. Clone or download this repository.

   ```bash
   git clone https://github.com/YOUR-USERNAME/Marauder-C5.git
   ```

2. Open the project source file in Arduino IDE.

3. Install the required libraries.

4. Select your ESP32-C5 board from **Tools → Board**.

5. Verify the pin configuration against your hardware.

6. Connect the peripherals and select the correct serial port.

7. Compile and upload the firmware.

8. Open the Serial Monitor at **115200 baud** to inspect initialization messages.

9. After startup, use the touchscreen menu to access the available tools.

> Replace `YOUR-USERNAME` and `Marauder-C5` in the clone URL with your actual GitHub username and repository name.

## Touchscreen Calibration

The current source code uses the following default calibration values:

```cpp
#define TS_MINX 200
#define TS_MAXX 3800
#define TS_MINY 200
#define TS_MAXY 3800
#define TS_INVERT_X true
#define TS_INVERT_Y true
```

If touch coordinates do not match the displayed buttons, recalibrate the touchscreen and adjust the inversion settings.

## Current Limitations

* BLE scan and advertising APIs can differ between NimBLE-Arduino versions.
* Some ESP32-C5 board configurations may not support every GPIO assignment used in this example.
* Raw Wi-Fi frame transmission depends on the ESP-IDF version, Wi-Fi interface state, and hardware support.
* The deauthentication monitor listens on a configured channel; it does not automatically monitor every Wi-Fi channel simultaneously.
* The NRF24L01 packet counter only detects compatible traffic that the module can receive. It is not a general-purpose Wi-Fi packet counter.
* The current event logger stores messages in RAM and does not provide persistent storage.
* The touchscreen calibration values may need adjustment for different display modules.

This is an experimental project. Individual features should be tested independently on the target hardware.

## Safety and Responsible Use

This project is intended for **education, research, and authorized testing**.

* Use wireless monitoring features only on networks and devices you own or have explicit permission to test.
* Do not interfere with third-party wireless communications.
* Do not use beacon or advertising experiments to mislead users or disrupt nearby devices.
* Follow applicable radio regulations and local laws.
* Be aware that wireless monitoring may collect device identifiers or other metadata.

The author does not encourage unauthorized access, interference, or disruption of wireless networks.

## Roadmap

Potential future improvements:

* [ ] Touchscreen calibration utility
* [ ] Improved BLE device information display
* [ ] Persistent event logging to a storage device
* [ ] Configurable channel selection
* [ ] Better error handling and peripheral diagnostics
* [ ] Improved display layout and navigation
* [ ] Build and compatibility documentation for supported ESP32-C5 boards

## Contributing

Contributions, bug reports, and suggestions are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Commit your changes.
4. Open a pull request describing your improvements.

Please include hardware details, ESP32 board package version, library versions, and relevant serial output when reporting a bug.

## License

This project is released under the MIT License. Add a `LICENSE` file to the repository if you intend to distribute it under that license, and make sure you have the rights to license all included code.

## Author

**YOUR-USERNAME**

GitHub: https://github.com/YOUR-USERNAME

---

*Built for embedded systems experimentation, wireless analysis, and learning.*
