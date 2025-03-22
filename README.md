# ESP32 + W5500 WebServer

## Overview
This project sets up an ESP32 microcontroller with a W5500 Ethernet module to run a web server. The server allows control and monitoring of connected devices via a REST API.

## Features
- WebServer on ESP32 with W5500 Ethernet module
- Static IP configuration
- REST API for controlling connected devices
- Support for SPI clock speed adjustment for stable communication

## Hardware Requirements
- ESP32 (Wroom Module or similar)
- W5500 Ethernet Module

## Software Requirements
- Arduino IDE
- ESP32 Board Package (Latest version)
- Required libraries:
  - `WebServer_ESP32_W5500`
  - `Ethernet`
  - `WiFi`
  
## Wiring Configuration
| W5500 Pin | ESP32 Pin |
|-----------|----------|
| SCLK      | GPIO 19  |
| MISO      | GPIO 23  |
| MOSI      | GPIO 26  |
| CS        | GPIO 27  |
| INT       | GPIO 22  |
| RESET     | GPIO 18  |

## Installation & Setup
1. **Install Arduino IDE** (if not installed already).
2. **Install ESP32 Board Package**:
   - Open Arduino IDE.
   - Go to `File` > `Preferences`.
   - Add `https://dl.espressif.com/dl/package_esp32_index.json` to "Additional Board Manager URLs".
   - Go to `Tools` > `Board` > `Boards Manager`.
   - Search for `ESP32` and install the latest version.
3. **Install Required Libraries**:
   - Open `Sketch` > `Include Library` > `Manage Libraries`.
   - Search for `WebServer_ESP32_W5500` and install it.
   - Install `Ethernet` and `WiFi` libraries.
4. **Upload Code**:
   - Open the Arduino sketch.
   - Select your board (`ESP32 Wrover Module`).
   - Connect the ESP32 and upload the code.

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

### Connection Issues
- Verify the W5500 wiring.
- Check if the router allows static IP assignments.

## License
This project is open-source and licensed under the MIT License.

---
Made with ❤️ by [Akmal Fadli]

