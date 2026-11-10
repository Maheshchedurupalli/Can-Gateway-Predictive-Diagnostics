# CAN Gateway with Predictive Diagnostics

> A two-node automotive CAN gateway: an STM32 (FreeRTOS) node reads and publishes vehicle-style signals over CAN, and an Embedded Linux node (SocketCAN) analyses them for early fault indicators and forwards telemetry over MQTT.

![Status](https://img.shields.io/badge/status-in%20progress-yellow)
![MCU](https://img.shields.io/badge/MCU-STM32-blue)
![RTOS](https://img.shields.io/badge/RTOS-FreeRTOS-green)
![Bus](https://img.shields.io/badge/bus-CAN%202.0B-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

<!-- Replace with a demo GIF or photo of the hardware setup -->
<!-- ![Demo](docs/images/demo.gif) -->

---

## Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [System Architecture](#system-architecture)
4. [Hardware](#hardware)
5. [Software Stack](#software-stack)
6. [Repository Structure](#repository-structure)
7. [Getting Started](#getting-started)
8. [CAN Message Map](#can-message-map)
9. [Predictive Diagnostics](#predictive-diagnostics)
10. [Telemetry (MQTT)](#telemetry-mqtt)
11. [Testing](#testing)
12. [Results](#results)
13. [Roadmap](#roadmap)
14. [What I Learned](#what-i-learned)
15. [License](#license)
16. [Contact](#contact)

---

## Overview

**Problem:** <!-- 1-2 lines: why a gateway + predictive diagnostics? e.g. detecting abnormal bus/ECU behaviour before it becomes a fault. -->

**Approach:** <!-- 2-3 lines: STM32 node handles real-time CAN I/O under FreeRTOS; Linux node does analysis and cloud forwarding. -->

**Outcome:** <!-- One measurable result once available, e.g. "Sustained 500 kbps with 0 lost frames over 1 hr; fault flagged X ms before threshold." -->

## Features

- [ ] Real-time CAN transmit/receive on STM32 using FreeRTOS tasks and queues
- [ ] CAN node on Embedded Linux using SocketCAN
- [ ] Gateway logic: filtering, routing and message translation
- [ ] Predictive diagnostics on signal trends
- [ ] MQTT telemetry publishing (TCP/IP)
- [ ] Error handling: bus-off recovery, error counters, watchdog

*(Tick items off as you finish them.)*

## System Architecture

<!-- Add a block diagram at docs/images/architecture.png -->

```
 [Sensors / simulated ECU signals]
              │
        ┌─────▼──────┐   CAN bus   ┌──────────────────┐   MQTT/TCP   ┌──────────┐
        │ STM32 node │◄──────────►│ Embedded Linux   │────────────►│  Broker  │
        │ (FreeRTOS) │  500 kbps   │ node (SocketCAN) │              │ / Dashboard │
        └────────────┘             └──────────────────┘              └──────────┘
```

| Layer | Responsibility |
|---|---|
| STM32 (FreeRTOS) | Signal acquisition, CAN frame TX/RX, task scheduling |
| Linux node | CAN capture, diagnostics analysis, telemetry |
| Cloud / broker | Telemetry ingestion and visualisation |

## Hardware

| Component | Qty | Purpose |
|---|---|---|
| STM32 board (`<model>`) | 1 | CAN node running FreeRTOS |
| Linux board (`<model>`) | 1 | Gateway / diagnostics node |
| MCP2515 + TJA1050/MCP2551 CAN module | `<n>` | CAN controller + transceiver |
| 120 Ω termination resistors | 2 | Bus termination |
| Jumper wires, breadboard, power supply | – | – |

**Wiring:** <!-- Add a wiring diagram/pin table in docs/hardware.md -->

## Software Stack

- **Firmware:** C, STM32 HAL/LL, FreeRTOS
- **Linux:** SocketCAN, `can-utils`, Python or C/C++ for the gateway app
- **Messaging:** MQTT (e.g. Mosquitto)
- **Tools:** `<IDE>`, `<debugger>`, `<CAN analyser>`, Git

## Repository Structure

```
.
├── firmware/            # STM32 FreeRTOS project
│   ├── Core/
│   └── Drivers/
├── gateway/             # Embedded Linux application
├── diagnostics/         # Predictive analysis logic
├── dbc/                 # CAN database (message definitions)
├── docs/
│   ├── images/
│   └── hardware.md
├── tests/
├── .gitignore
├── LICENSE
└── README.md
```

## Getting Started

### Prerequisites
- `<toolchain, e.g. arm-none-eabi-gcc / STM32CubeIDE>`
- Linux board with CAN interface enabled
- `can-utils`, MQTT broker

### 1. Build and flash the STM32 firmware
```bash
# Example, adjust to your setup
cd firmware
make
# flash with ST-Link / OpenOCD
```

### 2. Bring up the CAN interface on Linux
```bash
sudo ip link set can0 up type can bitrate 500000
candump can0
```

### 3. Run the gateway application
```bash
cd gateway
# build / run command here
```

## CAN Message Map

| ID (hex) | Name | DLC | Period | Signals |
|---|---|---|---|---|
| `0x100` | `<e.g. ENGINE_STATUS>` | 8 | 10 ms | `<rpm, temp, ...>` |
| `0x200` | `<e.g. DIAG_FLAGS>` | 4 | 100 ms | `<flags>` |

Full definitions: [`dbc/`](dbc/)

## Predictive Diagnostics

**Method:** <!-- e.g. moving average / threshold drift / simple trend detection -->
**Signals monitored:** <!-- list -->
**Output:** <!-- warning flag over CAN + MQTT alert -->

## Telemetry (MQTT)

| Topic | Payload | Rate |
|---|---|---|
| `gateway/<id>/signals` | JSON | `<n>` Hz |
| `gateway/<id>/alerts` | JSON | on event |

## Testing

- Bus load and frame-loss test: <!-- method + result -->
- Fault injection (error frames, disconnected node): <!-- result -->
- Latency measurement (STM32 → MQTT): <!-- result -->

## Results

<!-- Add measured numbers, screenshots, logic-analyser captures, dashboard images. -->

| Metric | Value |
|---|---|
| Bus bitrate | 500 kbps |
| Frame loss | `<n>` |
| End-to-end latency | `<ms>` |

## Roadmap

- [ ] Hardware bring-up and loopback test
- [ ] Two-node communication
- [ ] Gateway routing
- [ ] Diagnostics module
- [ ] MQTT telemetry
- [ ] Documentation and demo video
- [ ] *(Stretch)* UDS diagnostic services, AUTOSAR-style layering

## What I Learned

<!-- 3-5 bullets: e.g. CAN arbitration and error handling, FreeRTOS task design, SocketCAN, debugging with a logic analyser. -->

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE).

## Contact

**Mahesh Chedurupalli (Mahi)** · Embedded Systems Engineer
[LinkedIn](https://www.linkedin.com/in/mahesh-chedurupalli-010453288/) · [GitHub](https://github.com/Maheshchedurupalli)
