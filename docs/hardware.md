# Hardware

Hardware planned for the CAN gateway project. Models marked `TBD` will be updated as I finalise them.

## Nodes

| Node | Board | Role |
|---|---|---|
| Node 1 | STM32 development board (`TBD`) | CAN node running FreeRTOS: signal acquisition, CAN TX/RX |
| Node 2 | Embedded Linux board (`TBD`) | Gateway: SocketCAN capture, diagnostics, MQTT telemetry |

## CAN interface

| Component | Purpose |
|---|---|
| CAN transceiver (`TBD`, e.g. TJA1050 / MCP2551) | Converts CAN controller signals to the differential CAN bus |
| CAN controller (`TBD`, e.g. MCP2515 module, or the STM32's built-in bxCAN) | Frame handling and arbitration |
| 120 Ω resistors (x2) | Bus termination at each end |

## Bus settings

- Bitrate: 500 kbps
- Protocol: CAN 2.0B
- Topology: two nodes, twisted pair CANH/CANL

## Wiring

Pin connection tables and a wiring diagram will be added here once the setup is built.

## Tools

- ST-Link debugger/programmer
- USB-to-CAN adapter or logic analyser for monitoring the bus (`TBD`)
- Bench power supply / USB power
