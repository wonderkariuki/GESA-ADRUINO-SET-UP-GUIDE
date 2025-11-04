# Arduino IDE Library Installation Guide

To use the CanSat MQTT Telemetry system, you need to install the following libraries in Arduino IDE:

## Required Libraries

### 1. PubSubClient (MQTT Client)
- **Author:** Nick O'Leary
- **Installation:** Arduino IDE → Tools → Manage Libraries → Search "PubSubClient" → Install

### 2. DHT Sensor Library
- **Author:** Adafruit
- **Installation:** Arduino IDE → Tools → Manage Libraries → Search "DHT sensor library" → Install
- **Note:** This will also install the "Adafruit Unified Sensor" dependency

### 3. Adafruit BMP085 Library
- **Author:** Adafruit
- **Installation:** Arduino IDE → Tools → Manage Libraries → Search "Adafruit BMP085" → Install

### 4. MPU6050_light
- **Author:** rfetick
- **Installation:** Arduino IDE → Tools → Manage Libraries → Search "MPU6050_light" → Install

### 5. ArduinoJson
- **Author:** Benoit Blanchon
- **Installation:** Arduino IDE → Tools → Manage Libraries → Search "ArduinoJson" → Install

### 6. WiFi Library (Built-in)
- **Note:** This comes pre-installed with ESP32 board package

### 7. Wire Library (Built-in)
- **Note:** This comes pre-installed with Arduino IDE

## ESP32 Board Package Installation

If you haven't installed the ESP32 board package:

1. Go to **File → Preferences**
2. In "Additional Board Manager URLs" add:
   ```
   https://dl.espressif.com/dl/package_esp32_index.json
   ```
3. Go to **Tools → Board → Boards Manager**
4. Search for "ESP32" and install "ESP32 by Espressif Systems"

## Hardware Connections

### DHT11/DHT22 (Temperature & Humidity)
- VCC → 3.3V
- GND → GND
- DATA → GPIO 18

### BMP180 (Pressure & Temperature)
- VCC → 3.3V
- GND → GND
- SDA → GPIO 21
- SCL → GPIO 22

### MPU6050 (Accelerometer & Gyroscope)
- VCC → 3.3V
- GND → GND
- SDA → GPIO 21
- SCL → GPIO 22

## Configuration

Before uploading the code:

1. **Update WiFi Credentials:**
   ```cpp
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";
   ```

2. **Update MQTT Broker IP:**
   ```cpp
   const char* mqtt_server = "192.168.1.100";  // Your computer's IP
   ```

3. **Find Your Computer's IP Address:**
   - Windows: Open Command Prompt → Type `ipconfig`
   - macOS/Linux: Open Terminal → Type `ifconfig`
   - Look for your local IP address (usually starts with 192.168.x.x)

## Upload Process

1. Connect ESP32 to your computer via USB
2. Select **Tools → Board → ESP32 Dev Module**
3. Select the correct **Port** (usually COM3, COM4, etc. on Windows)
4. Click **Upload** button
5. Open **Serial Monitor** at 115200 baud rate to see debug output

## Troubleshooting

### Common Issues:

1. **"Library not found" errors:**
   - Make sure all required libraries are installed
   - Restart Arduino IDE after installing libraries

2. **WiFi connection fails:**
   - Double-check SSID and password
   - Make sure ESP32 is within WiFi range

3. **MQTT connection fails:**
   - Verify the MQTT broker IP address is correct
   - Make sure the MQTT broker is running on your computer
   - Check firewall settings

4. **Sensor not detected:**
   - Check wiring connections
   - Verify sensor power (3.3V, not 5V for most sensors)
   - Try different GPIO pins if needed

## Serial Monitor Output

When everything is working correctly, you should see output like:
```
🚀 CanSat MQTT System Starting Up
[OK] DHT sensor initialized
[OK] MPU6050 connected
[OK] BMP180 connected
WiFi connected!
✅ MQTT broker is reachable!
Connected to MQTT broker!
✅ Telemetry sent successfully
```
