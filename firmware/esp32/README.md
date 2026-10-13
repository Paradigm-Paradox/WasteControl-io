# ESP32 Edge Sensor Firmware for WasteControl-io

This directory contains turnkey ESPHome configurations for hardware monitoring of outdoor bins and waste streams.

## Configurations

1. **`bin_ultrasonic_distance.yaml`**:
   - **Target Hardware**: ESP32-C3 / ESP32-S3 + A02YYUW or JSN-SR04T waterproof ultrasonic sensor.
   - **Mounting**: Mounted underside of the bin lid facing down towards contents.
   - **Features**: Measures empty distance to waste, calculates fill percentage, reports battery level, and enters deep sleep for ultra-long battery runtime.

2. **`bin_ble_presence_tracker.yaml`**:
   - **Target Hardware**: ESP32 or BLE Beacon tag (e.g. BlueCharm / Nordic nRF52810 / ESP32-C3).
   - **Features**: Advertises iBeacon / BTHome payloads to indicate whether the bin is at the curbside beacon zone or inside the home storage bay.
