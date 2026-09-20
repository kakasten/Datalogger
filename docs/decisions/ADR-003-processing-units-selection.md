# ADR-003: Processing Units Selection

## Status

Accepted

## Context

The Datalogger requires two processing roles with different responsibilities:

- A Master processing unit for high-level processing, data logging, telemetry, and system management.
- A Slave microcontroller for local sensor acquisition, signal processing, and CAN communication.

The selected components must be recorded as part of the project's baseline hardware definition so that hardware, firmware, and future design decisions use the same references.

## Decision

The project will use the following processing units:

| System role | Component | Abbreviation |
| --- | --- | --- |
| Master | Milk-V DUO S | MPU (Microprocessor Unit) |
| Slave | STM32G431C8T6TR | MCU (Microcontroller Unit) |

The Milk-V DUO S is responsible for the Master module's high-level processing and data-management functions. The STM32G431C8T6TR is responsible for local acquisition and processing in the Slave modules.

## Consequences

### Positive

- Establishes a single hardware reference for the Master and Slave processing units.
- Allows hardware and firmware documentation to target defined components.
- Preserves the separation between high-level processing and deterministic local acquisition.

### Negative

- The Master software and hardware integration become dependent on the Milk-V DUO S platform.
- Slave firmware and hardware become dependent on the STM32G431C8T6TR device and its development ecosystem.

## Related Decisions

- [ADR-001: Distributed Datalogger Architecture](../getting-started/ADR-001-distributed-datalogger-architecture.md)
- [ADR-002: Slave MCU Selection](../getting-started/ADR-002-slave-mcu-selection.md)
