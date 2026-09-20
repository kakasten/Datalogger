# ADR-001: Distributed Datalogger Architecture

## Status

Accepted

## Context

The Datalogger system needs to acquire data from multiple sensors distributed throughout the vehicle.

A centralized architecture would require most sensors to be connected directly to a single processing unit. This would increase the amount of wiring throughout the vehicle and concentrate sensor acquisition, processing, and communication responsibilities in one location.

The system should provide:

* Scalable sensor acquisition
* Reduced wiring complexity
* Deterministic data acquisition
* Reliable communication between modules
* Easy expansion for additional sensors
* Separation between sensor acquisition and high-level data processing
* Independent development and testing of acquisition modules

Two main architectures were considered:

1. **Centralized architecture** — all sensors are connected directly to a single Master.
2. **Distributed architecture** — sensor acquisition is divided between multiple Slave modules connected to a central Master.

## Decision

The Datalogger will use a **distributed architecture** composed of:

* A **Master** responsible for high-level processing, data aggregation, storage, and external communication.
* Multiple **Slaves** responsible for local sensor acquisition, signal conditioning, preprocessing, and communication with the Master.
* A communication bus connecting the Master and Slaves.

Each Slave will be positioned according to the physical distribution and requirements of the sensors it handles.

The number and exact placement of Slaves will be defined based on sensor distribution, wiring requirements, acquisition requirements, and communication bandwidth.

## Alternatives Considered

### Centralized Architecture

All sensors would be connected directly to the Master.

**Advantages:**

* Simpler logical architecture
* Fewer electronic modules
* Centralized firmware

**Disadvantages:**

* Large amount of wiring throughout the vehicle
* Longer sensor connections
* More complex harness
* Less modular sensor acquisition
* Greater concentration of I/O requirements in the Master

### Distributed Architecture

Sensors are divided between multiple Slave modules connected to the Master.

**Advantages:**

* Reduced sensor wiring
* Modules can be positioned close to their sensors
* Modular hardware
* Easier expansion
* Separation of acquisition and high-level processing
* Easier reuse of Slave designs

**Disadvantages:**

* More electronic modules
* Requires a communication network
* Requires synchronization and communication management
* Increased firmware complexity

## Consequences

### Positive

* The system can scale by adding additional Slave modules.
* Sensor wiring can be significantly reduced by placing Slaves near their respective sensors.
* Sensor acquisition responsibilities are distributed across multiple modules.
* Hardware and firmware can be developed and tested in modular units.
* Different Slave configurations can support different sensor subsystems.

### Negative

* The communication network becomes a critical part of the architecture.
* Additional hardware is required for each Slave.
* Firmware must handle communication, synchronization, configuration, and fault detection between modules.
* The system requires careful management of communication bandwidth and message priorities.

## Related Decisions

This decision will influence subsequent ADRs, including:

* Master MPU selection
* Slave MCU selection
* Communication protocol selection
* CAN bus bandwidth and message architecture
* Slave physical distribution
* Sensor acquisition architecture
* Power architecture
* Firmware architecture
* Slave configuration architecture

## Notes

This ADR defines the high-level system architecture. Specific implementation details and component selections should be documented in separate ADRs or architecture documents.
