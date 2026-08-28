# Datalogger

The **Datalogger** is a distributed data acquisition and telemetry system developed for the Ampera Racing vehicle.

The system is designed to collect data from sensors distributed throughout the vehicle, process the measurements locally, and communicate the data through a reliable automotive network.

The project is divided into **Master** and **Slave** modules, allowing sensor acquisition to be distributed across the vehicle instead of concentrating all connections in a single board.

## System Overview

The Datalogger consists of:

* **Master** — central system responsible for data management, communication and higher-level processing.
* **Slave** — distributed acquisition module responsible for reading sensors and communicating with the Master.
* **CAN Network** — communication backbone between the modules.
* **Sensors** — analog, digital, frequency-based and digital-protocol sensors distributed throughout the vehicle.

```text
                    ┌───────────────┐
                    │     Master    │
                    │               │
                    └───────┬───────┘
                            │
                           CAN
                ┌───────────┴───────────┐
                │                       │
         ┌──────▼──────┐         ┌──────▼──────┐
         │   Slave 1   │         │   Slave 2   │
         │             │         │             │
         │   Sensors   │         │   Sensors   │
         └─────────────┘         └─────────────┘
```

## Documentation

The documentation is organized according to the main areas of the Datalogger system.

### Architecture

Architecture documentation describes the system design and the engineering decisions behind it.

* [Sampling Rates](architecture/sampling_rates.md)

### Hardware

Documentation related to the electronic design and PCB implementation.

> Hardware documentation is currently under development.

### Firmware

Documentation related to the embedded software running on the Datalogger modules.

> Firmware documentation is currently under development.

### Communication

Documentation related to the communication interfaces and protocols used by the Datalogger.

> Communication documentation is currently under development.

## Project Status

The Datalogger is currently under active development.

Hardware, firmware and system documentation may change as the design evolves and new requirements are established.

---

**Datalogger — Ampera Racing**
