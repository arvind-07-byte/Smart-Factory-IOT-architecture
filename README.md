# Smart--Factory-IOT-architecture


# Smart Factory IoT Architecture

## Project Description
This repository contains the cloud architecture, rule engine logic, and dashboard configurations for a distributed Smart Factory IoT Monitoring System. Designed for industrial environments, this project demonstrates how to route edge-device telemetry to a cloud platform using MQTT protocols for real-time visualization, automated hazard response, and remote actuator control.



## System Architecture
The system is built on a standard 3-Tier IoT architecture, connecting physical environments to cloud-based intelligence:

### 1. Edge Node Layer (Perception)
*   **Production Line Node:** Simulates continuous monitoring of heavy machinery. Processes metrics including ambient temperature, humidity, machine surface temperature, and vibration levels.
*   **Warehouse Node:** Monitors environmental stability and security. Processes metrics including ambient light levels, motion detection, door access, and climate data.

### 2. Transport Layer (Network)
*   **Protocol:** MQTT v3.1.1 over TCP/IP.
*   **Data Flow:** Nodes serialize telemetry into JSON payloads and publish to the cloud broker at continuous intervals.
*   **Reliability:** Implements automatic reconnection loops to maintain system integrity during network drops.

### 3. Application Layer (ThingsBoard Cloud)
*   **Data Visualization:** Live interactive dashboards displaying real-time gauges, time-series charts, and binary status indicators.
*   **Automated Rule Engine:** Processes incoming data against strict industrial thresholds. 
    *   *Example:* If warehouse humidity exceeds critical levels, the system automatically routes an activation signal to the ventilation relay without human intervention.
    *   *Example:* Temperature breaches trigger instant system-wide critical alarms and localized LED warnings.
*   **Remote Procedure Call (RPC):** Enables operators to manually override local edge logic and control actuators (e.g., emergency relay shutdowns) directly from the cloud interface.

