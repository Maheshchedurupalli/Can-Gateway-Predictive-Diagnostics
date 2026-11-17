# CAN Basics (notes for this project)

## What CAN is
Controller Area Network (CAN) is a two-wire, multi-node serial bus used in vehicles. Any node can send; there is no master.

## Frame fields (CAN 2.0)

| Field | Purpose |
|---|---|
| SOF | Start of frame (1 dominant bit) |
| Identifier | 11 bits (standard) or 29 bits (extended). Also sets priority |
| RTR / IDE | Remote request and standard/extended flags |
| DLC | Data length, 0 to 8 bytes |
| Data | The signals (see `dbc/gateway.dbc`) |
| CRC | 15-bit checksum for error detection |
| ACK | Receivers pull this bit dominant to confirm a good frame |
| EOF | End of frame (7 recessive bits) |

## Arbitration
- The bus has two levels: dominant (0) and recessive (1). Dominant wins.
- When two nodes send at once, each compares the bit it sends with the bit on the bus. The node that sends a recessive bit and reads a dominant one stops.
- So the **lower ID wins**. Example: `0x100` has priority over `0x200`.
- The winner's frame is not damaged and no time is lost.

## Bit stuffing
After five identical bits in a row, the sender inserts one opposite bit. This keeps edges on the bus so nodes stay synchronised. Receivers remove the extra bits.

## Error handling
- Each node keeps a transmit error counter (TEC) and receive error counter (REC).
- **Error active:** normal operation.
- **Error passive:** a counter is 128 or higher, so the node is more restricted.
- **Bus-off:** TEC goes above 255, so the node leaves the bus until it recovers.
- This is why the firmware plan includes bus-off recovery.

## Physical layer
- Two wires: CANH and CANL, a twisted pair.
- A 120 ohm resistor at each end of the bus. Measured with power off, CANH to CANL should read about 60 ohm.

## This project's settings
- Bitrate: 500 kbps, so each bit lasts 2 microseconds.
- A standard frame with 8 data bytes is about 110 bits before stuffing.
- Messages: `ENGINE_STATUS` (0x100) and `DIAG_FLAGS` (0x200).
