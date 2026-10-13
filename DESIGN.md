# WasteControl-io: Design & Architecture Document

## Overview
**WasteControl-io** is an edge-native Home Assistant Add-on providing automated municipal and private collection schedule coordination, IoT smart bin telemetry, stream sorting logistics, and homestead waste loop management.

For full architectural details, mathematical fill models, and subsystem specifications, see [docs/DESIGN.md](docs/DESIGN.md).

## Core Capabilities
1. **Dynamic Collection Scheduling & Holiday Intelligence**:
   - Multi-stream cadence engine (weekly, bi-weekly odd/even, monthly, custom).
   - Automated municipal holiday delay rules (+1 day shifts) and iCal synchronization.
   - Proactive actionable alerts ("Take cans to the curb", "Bring cans back in").

2. **Smart Bin Telemetry & Location Tracking**:
   - Continuous fill percentage monitoring calculated from container depth vs. ultrasonic/ToF sensor distance.
   - Tri-state location tracking (`storage`, `curb`, `transit`) via BLE beacons, RFID, or contact switches.
   - Lid status and tilt sensing to detect emptied cans and open-lid rain alerts.

3. **Homestead Waste Routing & Composting Integration**:
   - Organic kitchen scrap routing into compost bays (integrating with `CompostControl-io`).
   - Hazardous materials, e-waste, and battery accumulation limit tracking.
   - Septic tank pumping cycle intervals and holding tank alarms.

4. **ESP32 Distributed Edge Microcontrollers**:
   - Turnkey ESPHome firmware configurations for weatherproof battery/solar-powered bin monitors.
   - Ultra-low-power deep sleep cycles with ultrasonic ping and accelerometer motion wakeups.

5. **Integrated Ingress Web Dashboard**:
   - Responsive dark-themed control center accessible directly within Home Assistant's sidebar.
   - Visual fill gauges, countdown timers, and quick one-tap location overrides (`At Curb`, `At Storage`).

## Project Structure
- `repository.yaml` — Repository manifest for the Home Assistant Add-on Store.
- `waste_control/` — Complete add-on distribution.
  - `config.yaml` — Add-on definition, options schema, and ingress settings.
  - `Dockerfile` — Multi-arch Alpine container.
  - `build.yaml` — Multi-architecture build definitions (`aarch64`, `amd64`, `armv7`).
  - `run.sh` — Add-on startup entrypoint with bashio logging.
  - `app/` — Core Python FastAPI backend and responsive Ingress web dashboard.
    - `engine/` — Schedule calculations, bin state manager, and MQTT discovery publisher.
- `firmware/` — ESP32 edge microcontroller firmware configurations (ESPHome).
  - `esp32/bin_ultrasonic_distance.yaml` — Weatherproof ultrasonic bin fill monitor.
  - `esp32/bin_ble_presence_tracker.yaml` — BLE curb presence beacon.
- `docs/` — In-depth architectural specifications and user documentation.
