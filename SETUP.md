# CanSat Base Station Quick Setup Guide

## Step 1: Install MQTT Broker

### Option A: Install Mosquitto (Recommended)
```powershell
# Using Chocolatey (recommended)
choco install mosquitto

# Or download from: https://mosquitto.org/download/
```

### Option B: Use Docker
```powershell
docker run -it -p 1883:1883 eclipse-mosquitto
```

## Step 2: Find Your Computer's IP Address
```powershell
ipconfig
```
Look for your WiFi adapter's IPv4 address (e.g., 192.168.1.100)

## Step 3: Update CanSat Code
In `src/main.cpp`, change the MQTT server to your computer's IP:
```cpp
const char* mqtt_server = "192.168.1.XXX";  // Your computer's IP
```

## Step 4: Start the System

### Terminal 1: Start MQTT Broker
```powershell
cd base_station
.\start_mqtt_broker.bat
```

### Terminal 2: Start Base Station
```powershell
cd base_station
.\start_base_station.bat
```

### Terminal 3: Upload to ESP32
```powershell
pio run --target upload
pio device monitor
```

## Quick Test Commands

Once the base station is running, you can send commands:
- `status` - Get CanSat status
- `calibrate` - Calibrate MPU6050
- `reset` - Reset sensor flags

## Troubleshooting

**CanSat can't connect to MQTT:**
1. Make sure WiFi credentials are correct
2. Check that your computer and ESP32 are on the same network
3. Verify the IP address in the CanSat code
4. Make sure MQTT broker is running

**Base station shows connection refused:**
1. Start the MQTT broker first
2. Check if port 1883 is open
3. Try using localhost or 127.0.0.1

**No data received:**
1. Check serial monitor for ESP32 errors
2. Verify MQTT topics match
3. Check WiFi connection on ESP32

## Data Format

The CanSat sends JSON data like this:
```json
{
  "cansat_id": "CANSAT_001",
  "timestamp": 12345,
  "temperature_dht": 23.5,
  "humidity": 65.2,
  "temperature_bmp": 23.8,
  "pressure": 1013.25,
  "altitude": 150.5,
  "accel_x": 0.12,
  "accel_y": -0.05,
  "accel_z": 9.81,
  "rssi": -45,
  "sensor_status": {
    "dht": true,
    "bmp": true,
    "mpu": true
  }
}
```
