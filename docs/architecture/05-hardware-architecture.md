# Hardware Architecture

## Objective

Describe the hardware architecture of the Datalogger system, including the responsibilities of each hardware module, sensor acquisition, signal conditioning, power distribution, and hardware interfaces.

---

## Overview

The Datalogger hardware is organized into distributed acquisition modules connected to a central Master module.

The Master provides the main processing and data management capabilities, while the Slave modules are responsible for acquiring vehicle sensor signals close to their physical installation points.

This distributed architecture reduces sensor wiring length, simplifies the integration of vehicle sensors, and allows the acquisition system to scale according to the requirements of the vehicle.

---

## System Hardware

The system is composed of two main hardware roles:

* Master
* Slave

The Master is based on a Microprocessor Unit (MPU), while each Slave uses a Microcontroller Unit (MCU) for local sensor acquisition and processing.

```text
                           ┌────────────────────────────┐
                           │          MASTER            │
                           │            MPU             │
                           │                            │
                           │  Processing                │
                           │  Data Logging              │
                           │  Telemetry                 │
                           │  System Management         │
                           └────────────┬───────────────┘
                                        │
                                   CAN Network
                                        │
                  ┌─────────────────────┴─────────────────────┐
                  │                                           │
       ┌──────────▼──────────┐                    ┌──────────▼──────────┐
       │       SLAVE A       │                    │       SLAVE B       │
       │         MCU         │                    │         MCU         │
       │                     │                    │                     │
       │ Signal Acquisition  │                    │ Signal Acquisition  │
       │ Signal Conditioning │                    │ Signal Conditioning │
       │ Local Processing    │                    │ Local Processing    │
       └──────────┬──────────┘                    └──────────┬──────────┘
                  │                                           │
           Vehicle Sensors                             Vehicle Sensors
```

---

## Master Module

### Master Purpose

The Master is the central processing and data management module of the Datalogger system.

### Master Responsibilities

* Receive data from Slave modules
* Process and manage acquired data
* Store vehicle data
* Manage system-level services
* Provide telemetry interfaces
* Provide external communication interfaces
* Coordinate system operation

### Master Hardware

The Master hardware is composed of:

* MPU
* Non-volatile storage
* CAN interface
* Ethernet interface
* USB interface
* Power management
* External communication interfaces

---

## Slave Module

### Slave Purpose

The Slave is a distributed sensor acquisition module responsible for acquiring and conditioning signals from vehicle sensors.

Multiple Slave modules can be deployed throughout the vehicle according to sensor location and acquisition requirements.

### Slave Responsibilities

* Acquire analog signals
* Acquire digital signals
* Measure frequency-based signals
* Perform signal conditioning
* Convert analog signals to digital measurements
* Perform local signal processing
* Transmit measurements to the Master
* Monitor local hardware status

### Slave Hardware

Each Slave is composed of:

* MCU
* ADC interfaces
* Signal conditioning circuits
* Digital input interfaces
* Frequency measurement interfaces
* CAN interface
* Local communication interfaces
* Power regulation and protection

---

## Sensor Acquisition

The Datalogger supports multiple types of vehicle sensor signals.

| Signal Type | Typical Application                   | Acquisition Module |
| ----------- | ------------------------------------- | ------------------ |
| Analog      | Pressure, temperature, potentiometers | Slave              |
| Digital     | Switches, status signals              | Slave              |
| Frequency   | Wheel speed, rotational sensors       | Slave              |
| CAN         | Vehicle ECUs and smart sensors        | Master / Slave     |
| I²C         | Local digital sensors                 | Slave              |

The acquisition hardware is designed to adapt the electrical characteristics of the vehicle sensors to the voltage and signal requirements of the MCU and peripheral devices.

---

## Signal Conditioning

Signal conditioning is performed locally within the Slave modules whenever possible.

Typical conditioning stages include:

```text
Vehicle Sensor
      │
      ▼
Protection
      │
      ▼
Signal Conditioning
      │
      ▼
Filtering
      │
      ▼
ADC / Digital Input
      │
      ▼
MCU
      │
      ▼
CAN Network
```

Signal conditioning may include:

* Overvoltage protection
* Input protection
* Voltage level adaptation
* Analog filtering
* Signal buffering
* Pull-up / pull-down networks
* Frequency signal conditioning

The specific conditioning circuit depends on the electrical characteristics of each sensor.

---

## Power Architecture

Power distribution is separated according to the requirements of the vehicle, sensors, and electronics.

The hardware architecture provides dedicated power domains for:

* Vehicle input power
* Sensor power
* Digital electronics
* Analog electronics
* Communication interfaces

The detailed power distribution and regulation strategy is documented separately in the Power Architecture document.

---

## Hardware Interfaces

The main hardware interfaces are:

| Interface | Hardware Role                   | Typical Usage                 |
| --------- | ------------------------------- | ----------------------------- |
| CAN       | Inter-module communication      | Master ↔ Slave                |
| I²C       | Local peripheral interface      | ADCs and sensors              |
| SPI       | High-speed peripheral interface | Memory and ADCs               |
| UART      | Point-to-point interface        | GNSS, IMU, debug              |
| Ethernet  | External high-speed interface   | Development and data transfer |
| USB       | External service interface      | Debugging and maintenance     |

The communication behavior and protocol-level definitions are described in the Communication Architecture document.

---

## Modularity

The hardware architecture is designed to allow modules to be added or modified without requiring major changes to the rest of the system.

Each Slave operates as an independent acquisition unit with a defined interface to the system.

This allows:

* Additional Slave modules
* Different sensor configurations
* Hardware revisions
* Independent module testing
* Reuse of acquisition hardware
* Simplified vehicle integration

---

## Hardware Design Principles

The hardware architecture follows these principles:

* Distributed sensor acquisition
* Modular hardware
* Short sensor wiring
* Local signal conditioning
* Electrical protection
* Clear separation of responsibilities
* Scalable number of acquisition modules
* Design for maintainability
* Design for testing
* Automotive-oriented robustness
