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

### Getting Started

Start here if you are new to the project.

* [Getting Started](getting-started.md)

### Requirements

System and module requirements define what the Datalogger must provide.

* [Slave Requirements](requirements/slave-requirements.md)

### Architecture

Architecture documents describe how the system is structured and how its components interact.

* [System Architecture](architecture/system.md)
* [Slave Architecture](architecture/slave.md)
* [Hardware Architecture](architecture/hardware.md)
* [Software Architecture](architecture/software.md)
* [Communication Architecture](architecture/communication.md)

### Hardware

Documentation related to the electronic design and PCB implementation.

* Schematic
* PCB
* Bill of Materials

### Firmware

Documentation related to the embedded software running on the Datalogger modules.

* Firmware Architecture
* Drivers
* Tasks and Scheduling

### Architecture Decisions

Important technical decisions are documented using Architecture Decision Records (ADRs).

* [Architecture Decision Records](adr/)

## Project Status

The Datalogger is currently under active development.

Hardware and firmware documentation may change as the design evolves and new requirements are established.

---

**Datalogger — Ampera Racing**
