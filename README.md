# ConvergeIoT MQTT Specification

This repository defines the MQTT communication standards for the **ConvergeIoT** project. It provides a unified interface between ESP32-based IoT nodes (called **node**) and the Go-based middleware (**gateway**).

## 🔧 Architecture Overview

[node] ←→ MQTT Broker ←→ [gateway] → Logging / Metrics / Integration

### Components
- **node**: ESP32/RPI2040 microcontroller with sensors and actuators
- **gateway**: Go middleware for processing, storage, and control
- **Broker**: MQTT routing
- **Storage/Monitoring**: time-series data and visualization (influx / grafana)

## 📡 MQTT Topic Structure

All topics follow a versioned and grouped schema:

iot/v1/{group}/{location}/{device_id}/{detail}


Examples:
- `iot/v1/metrics/livingroom/device-01/temperature`
- `iot/v1/commands/any/broadcast`
- `iot/v1/logs/default/node-99/config`

**Groups:**
- `metrics` – sensor data
- `commands` – control and configuration commands
- `logs` – system and configuration logs

**Special Locations:**
- `default` – newly joined devices without an assigned location
- `any` – reserved for broadcast commands only

## 📜 Documentation

Full communication is defined using **AsyncAPI 2.6**:

📄 [asyncapi/iot-v1.yaml](./asyncapi/iot-v1.yaml)

## 📂 Project Structure

convergeiot-mqtt-spec/
├── asyncapi/
│ └── iot-v1.yaml
├── schemas/
│ ├── metric.schema.json
│ ├── command.schema.json
│ ├── log.schema.json
├── examples/
│ ├── metric-temperature.json
│ ├── command-update-config.json
│ ├── command-firmware-update.json
│ └── log-config.json
└── README.md

## 🤝 Contributing

Pull requests are welcome! Please ensure:
- Consistent topic and payload structure
- All changes documented in AsyncAPI
- Add examples in `examples/`

## 🛡️ License

This project is licensed under the GNU General Public License v3.0 (GPLv3).  
See the full license text at [https://www.gnu.org/licenses/gpl-3.0.txt](https://www.gnu.org/licenses/gpl-3.0.txt)

