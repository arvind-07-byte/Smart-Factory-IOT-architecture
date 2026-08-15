# Smart Factory IoT Monitoring System

An end-to-end distributed IoT monitoring and supervisory control system built for industrial environments. This project simulates real-time data collection from a factory production line and a warehouse, utilizing MQTT for telemetry transport and ThingsBoard for cloud visualization, automated rule-engine alerts, and remote actuation.

## 🏭 Project Overview
Traditional industrial environments suffer from delayed incident response and reactive maintenance. This system solves these issues by providing real-time visibility, threshold-based automated control, and Remote Procedure Call (RPC) capabilities. 

The architecture consists of two edge nodes (Arduino Uno) simulated in PicsimLab, transmitting JSON payloads over Ethernet to a ThingsBoard Cloud MQTT Broker.

### Key Features
* **Distributed Monitoring:** Dual-node setup tracking Production Line (Node 1) and Warehouse (Node 2) environments.
* **Fault-Tolerant Edge Logic:** Implements sensor error handling (caching last-known-valid data on hardware failure) and PIR motion de-bouncing to prevent false cloud alarms.
* **Automated Actuation:** Warehouse node executes local logic to automatically trigger HVAC ventilation if humidity exceeds 85%.
* **Bidirectional RPC Control:** Cloud-to-device commands allow remote managers to manually override automation or trigger emergency machine shutdowns.
* **Cloud Rule Engine:** Server-side processing automatically generates and resolves `CRITICAL` and `WARNING` alarms based on telemetry thresholds.

---

## 🏗️ System Architecture

* **Perception Layer (Edge):** Arduino Uno (ATmega328P) via PicsimLab. Sensors include DHT22, LM35, PIR, LDR, Potentiometer, and Reed Switches.
* **Network Layer:** W5100 Ethernet interface publishing QoS 1 messages via MQTT v3.1.1 over TCP/IP (Port 1883).
* **Application/Cloud Layer:** ThingsBoard CE Cloud handling device authentication, PostgreSQL time-series storage, rule chains, and live dashboards.

---

## 🔌 Hardware Pin Mapping

### Node 1 (Production Line)
| Pin | Component | Description |
| :--- | :--- | :--- |
| **D2** | DHT22 | Ambient Temperature & Humidity |
| **D3** | Push Button | Machine State (Active LOW) |
| **D4** | Relay Module | Machine Power Control / Emergency Kill |
| **A0** | Potentiometer | Machine Vibration Simulator |
| **A1** | LM35 | Machine Surface Temperature |
| **D5, D6, D7** | LEDs | Status Indicators (Green/Yellow/Red) |

### Node 2 (Warehouse)
| Pin | Component | Description |
| :--- | :--- | :--- |
| **D2** | DHT22 | Ambient Temperature & Humidity |
| **D3** | HC-SR501 PIR | Motion Detection |
| **D4** | Relay Module | Ventilation / HVAC Control |
| **A0** | LDR | Ambient Light Level |
| **D7** | Reed Switch | Door Security State |

---

## 🛠️ Software & Dependencies
* **Platform:** PicsimLab (Arduino Uno target)
* **IoT Cloud:** [ThingsBoard Cloud](https://cloud.thingsboard.io/)
* **Core Libraries:**
  * `PubSubClient.h` (Note: `MQTT_MAX_PACKET_SIZE` must be modified to 256 bytes to handle the multi-key JSON payload).
  * `DHT.h`

---
