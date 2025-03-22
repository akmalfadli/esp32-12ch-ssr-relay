# ESP32 + W5500 WebServer

## Overview
The Wemos32 12-Channel SSR Relay Controller is a smart switching system based on the ESP32 development board. It utilizes Solid State Relays (SSR) for controlling AC loads and features an Ethernet module (W5500) for network communication. The design is optimized for industrial and home automation applications, offering secure, remote-controlled relay switching.

![alt text](https://github.com/akmalfadli/esp32-12ch-ssr-relay/blob/master/img/Pasted%20image.png?raw=true)

## Features
Features

- ESP32-based control with Wi-Fi and Ethernet connectivity.
- 12-channel SSR relay control using G3MB-202P relays.
- W5500 Ethernet module for reliable wired communication.
- OLED 0.96-inch display for status monitoring.
- Secure API for remote control using authentication.
- Power supply management with AMS1117 3.3V regulator.
- Fuse protection for safety.


![alt text](https://github.com/akmalfadli/esp32-12ch-ssr-relay/blob/master/img/esp32-12ch-ssr-relay.png?raw=true)

## Hardware Components
### 1. **Microcontroller**
- **ESP32-DEVKITC-32D** (provides Wi-Fi and Ethernet control)
- **Connected to W5500 Ethernet module** via SPI

### 2. **Relay Switching System**
- **12x G3MB-202P SSR relays** for AC load switching
- **Transistor drivers (SS8050)** for relay activation
- **LED indicators** for relay status

### 3. **Power Supply**
- **5V to 3.3V AMS1117 voltage regulator**
- **Multiple fuses for overcurrent protection**
- **External power input via barrel jack**

## Wiring Diagram
| Component | ESP32 Pin |
|-----------|----------|
| W5500 SPI MISO | GPIO 19 |
| W5500 SPI MOSI | GPIO 23 |
| W5500 SPI SCK  | GPIO 18 |
| W5500 SPI CS   | GPIO 5  |
| W5500 INT      | GPIO 4  |
| OLED SDA       | GPIO 21 |
| OLED SCL       | GPIO 22 |
| Relay 1-12     | GPIO 2, 16, 17, 13, 15, 14, 12, 25, 26, 33, 32, 27 |


## Installation & Setup
1. **Install Arduino IDE** (if not installed already).
2. **Install ESP32 Board Package**:
   - Open Arduino IDE.
   - Go to `File` > `Preferences`.
   - Add `https://dl.espressif.com/dl/package_esp32_index.json` to "Additional Board Manager URLs".
   - Go to `Tools` > `Board` > `Boards Manager`.
   - Search for `ESP32` and install the latest version.
3. **Install Required Libraries**
4. **Upload Code**:
   - Open the Arduino sketch.
   - Select your board (`ESP32 Wrover Module`).
   - Connect the ESP32 and upload the code.
   - Github repo for Arduino code [a link](https://github.com/akmalfadli/esp32-12ch-eth)

## Static IP Configuration
Modify the `setup()` function in your Arduino sketch:
```cpp
Ethernet.begin(mac, ip, myDns, gateway, subnet);
```
Example static IP settings:
```cpp
IPAddress ip(192, 168, 11, 51);
IPAddress gateway(192, 168, 11, 1);
IPAddress subnet(255, 255, 255, 0);
IPAddress myDns(8, 8, 8, 8);
```

## API Endpoints
| Method | Endpoint        | Description          |
|--------|----------------|----------------------|
| GET    | `/relay-state?ch=`      | Get device status   |
| POST   | `/relay?ch=2&state=0`    | Turn relay ON and OFF      |
| POST   | `set-auth?new-key`   |Set bearer token key     |

## Troubleshooting
### Compilation Errors
- **Ensure ESP32 is selected** in `Tools` > `Board`.
- **Check for duplicate libraries** in `Arduino/libraries/` and remove conflicting versions.
- **Reduce SPI clock speed** if Ethernet is unstable:
  ```cpp
  #define ETH_SPI_CLOCK 8000000  // Set to 8MHz
  ```

## Troubleshooting
- **No Ethernet Connection** → Check **W5500 wiring** and **IP settings**.
- **Relays not Switching** → Ensure **power supply** and **correct GPIO connections**.
- **OLED Display not Working** → Confirm **I2C address (default: 0x3C)**.

## Future Enhancements
- **Add MQTT for IoT integration**.
- **Web-based control panel** for easier relay management.
- **RTC for scheduled relay operations**.

## License
This project is open-source and licensed under the MIT License.

---
Made with ❤️ by Akmal Fadli - Perwira Teknologi Informasi

