```mermaid
graph TD
    subgraph EdgeLayer [Edge Layer: Perception & Actuation]
        N1["Node 1: Production Line<br>Sensors: DHT22, LM35, Vibration<br>Actuators: Production Relay, LEDs"]
        N2["Node 2: Warehouse<br>Sensors: DHT22, LDR, PIR, Reed Switch<br>Actuators: Ventilation Relay"]
    end

    subgraph TransportLayer [Transport Layer: Network & Protocol]
        MQTT["MQTT v3.1.1 Protocol<br>TCP/IP via Ethernet<br>JSON Payloads"]
    end

    subgraph ApplicationLayer [Application Layer: Cloud & UI]
        TB["ThingsBoard Cloud Platform<br>MQTT Broker, Rule Engine, Alarms"]
        DASH["User Interface Dashboard<br>Real-Time Gauges & RPC Control"]
    end

    %% Data Flow
    N1 -->|Publish Telemetry 5s| MQTT
    N2 -->|Publish Telemetry 5s| MQTT
    MQTT -->|Route to Port 1883| TB
    TB -->|WebSocket Updates| DASH

    %% Control Flow
    DASH -.->|RPC Command| TB
    TB -.->|RPC Routing| MQTT
    MQTT -.->|De-energize Relay| N1
    MQTT -.->|Activate Ventilation| N2
