# CAN Bus Budget

## Objective

Define the preliminary CAN bus budget for the Datalogger, including the expected message set, message priorities, and identifier allocation. This document is a baseline for firmware and hardware implementation and must be refined after the sensor list and timing requirements are finalized.

---

## Scope and Assumptions

The preliminary budget uses the following assumptions:

- The CAN bus connects one Master (Milk-V DUO S) to multiple Slave modules.
- Slaves use the STM32G431C8T6TR and support CAN FD.
- Standard 11-bit CAN identifiers are used.
- The identifier value determines arbitration priority: lower values have higher priority.
- The initial network target is up to 8 Slave modules.
- The initial nominal arbitration rate is 500 kbit/s.
- CAN FD data-phase configuration and payload sizes remain to be validated during bus-load testing.
- Message frequencies are preliminary engineering limits, not final sensor sampling rates.

The bus budget must be recalculated if the number of Slaves, message frequencies, payload sizes, or CAN bit rates change.

---

## Priority Classes

| Priority | Class | Use | Identifier range |
| --- | --- | --- | --- |
| P0 | Emergency and safety | Emergency events, watchdog, bus-critical faults | `0x000–0x07F` |
| P1 | Synchronization and control | Time synchronization, acquisition commands, operating state | `0x080–0x0FF` |
| P2 | High-rate acquisition | Fast sensor measurements and time-critical feedback | `0x100–0x1FF` |
| P3 | Normal acquisition | Standard analog, digital, and frequency measurements | `0x200–0x3FF` |
| P4 | Diagnostics and configuration | Health, configuration, identification, and diagnostics | `0x400–0x5FF` |
| P5 | Development and reserved | Development traffic and future extensions | `0x600–0x6FF` |

Identifiers from `0x700–0x7FF` are reserved for future use and must not be assigned without updating this document.

---

## Preliminary Identifier Map

The source field identifies the module that produces the message. The initial allocation supports module addresses `0x0–0xF`, allowing up to 16 addressed modules. `S` represents the Slave address.

| Identifier | Message | Direction | Frequency limit | Payload | Priority |
| --- | --- | --- | ---: | ---: | --- |
| `0x010` | Emergency event | Master / Slave → network | Event-driven | 8 bytes | P0 |
| `0x020 + S` | Slave watchdog/status fault | Slave → Master | Event-driven, max. 10 Hz | 8 bytes | P0 |
| `0x080` | Network time synchronization | Master → Slaves | 100 Hz | 8 bytes | P1 |
| `0x090` | Acquisition control | Master → Slaves | 50 Hz | 8 bytes | P1 |
| `0x0A0 + S` | Slave operating state | Slave → Master | 10 Hz | 8 bytes | P1 |
| `0x100 + S` | High-rate measurement group 0 | Slave → Master | 1 kHz | 16 bytes FD | P2 |
| `0x110 + S` | High-rate measurement group 1 | Slave → Master | 500 Hz | 16 bytes FD | P2 |
| `0x200 + S` | Analog measurement group 0 | Slave → Master | 100 Hz | 16 bytes FD | P3 |
| `0x210 + S` | Analog measurement group 1 | Slave → Master | 100 Hz | 16 bytes FD | P3 |
| `0x220 + S` | Digital and frequency inputs | Slave → Master | 100 Hz | 8 bytes | P3 |
| `0x230 + S` | Sensor status and timestamps | Slave → Master | 100 Hz | 16 bytes FD | P3 |
| `0x400 + S` | Slave health and diagnostics | Slave → Master | 1 Hz | 16 bytes FD | P4 |
| `0x410 + S` | Configuration response | Slave → Master | Event-driven | 16 bytes FD | P4 |
| `0x480` | Configuration command | Master → Slave | Event-driven | 16 bytes FD | P4 |
| `0x490` | Firmware/service command | Master → Slave | Event-driven | 16 bytes FD | P4 |
| `0x600` | Development trace | Master / Slave → network | Development only | 16 bytes FD | P5 |

For a given message family, `S` is the Slave address from `0x0` to `0xF`. The resulting identifier must remain inside the range assigned to that family.

---

## Preliminary Message Count

For the initial target of 8 Slaves, the periodic traffic budget is:

| Message family | Messages per Slave | Network total | Frequency per message | Aggregate rate |
| --- | ---: | ---: | ---: | ---: |
| Operating state | 1 | 8 | 10 Hz | 80 messages/s |
| High-rate group 0 | 1 | 8 | 1,000 Hz | 8,000 messages/s |
| High-rate group 1 | 1 | 8 | 500 Hz | 4,000 messages/s |
| Analog group 0 | 1 | 8 | 100 Hz | 800 messages/s |
| Analog group 1 | 1 | 8 | 100 Hz | 800 messages/s |
| Digital/frequency inputs | 1 | 8 | 100 Hz | 800 messages/s |
| Sensor status/timestamps | 1 | 8 | 100 Hz | 800 messages/s |
| Diagnostics | 1 | 8 | 1 Hz | 8 messages/s |
| **Total periodic traffic** | **8** | **64** | — | **15,288 messages/s** |

The high-rate rows are a capacity placeholder for the fastest acquisition use cases. They must not be enabled for every Slave until the bus-load calculation and measurements confirm that the selected bit rates provide sufficient margin.

Event-driven emergency, configuration, and service messages are excluded from the periodic total. Their maximum rates must be bounded by the firmware implementation.

---

## Bus-Load Budget

The preliminary design target is:

- Normal operating bus load: **≤ 50%**.
- Sustained worst-case bus load: **≤ 70%**.
- Emergency and diagnostic traffic must retain arbitration access under normal load.
- At least 30% capacity should remain for timing variation, retransmissions, future messages, and additional Slaves.

Bus load must be calculated using the complete on-wire frame size, including arbitration, control, CRC, acknowledgment, inter-frame spacing, bit stuffing, and the selected nominal/data bit rates. Payload byte count alone is not sufficient for this calculation.

The current message-rate table is therefore a message-count budget, not a validated utilization result.

---

## Allocation Rules

1. Lower CAN identifiers always represent higher arbitration priority.
2. Emergency and safety messages must use the P0 range.
3. Periodic sensor messages must include a source Slave address in their identifier.
4. A message family must keep the same payload layout and cycle time across all Slaves.
5. Event-driven messages must define rate limiting and timeout behavior in the protocol specification.
6. Identifier reuse is not allowed while two message types can coexist on the bus.
7. New identifiers must be added to this map before implementation.
8. Any change to message frequency or payload size requires repeating the bus-load calculation.

---

## Open Items

The following items remain to be defined before the CAN budget can be considered final:

- Final CAN nominal and data-phase bit rates.
- Exact number and type of sensors per Slave.
- Final sampling frequencies and required latency for each signal.
- Payload encoding, byte order, scaling, and timestamp format.
- Maximum number of Slaves in the vehicle.
- Bus termination and physical-layer validation.
- Measured bus load under nominal and worst-case traffic.
- Fault handling, retransmission, timeout, and node-offline behavior.

---

## Related Documentation

- [Communication Architecture](02-network.md)
- [Hardware Architecture](05-hardware-architecture.md)
- [ADR-001: Distributed Datalogger Architecture](../getting-started/ADR-001-distributed-datalogger-architecture.md)
