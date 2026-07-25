# Communication Architecture

## Objective

Describe the communication architecture of the Datalogger system, including the communication interfaces used between modules and peripherals.

---

## Overview

The Datalogger system uses multiple communication interfaces to connect distributed acquisition modules, sensors, and external devices. Each interface is selected according to bandwidth, latency, reliability, and hardware requirements.

The CAN bus serves as the system backbone, connecting the Master module to one or more Slave modules. Local peripherals communicate directly with each module using dedicated interfaces such as I²C, SPI, and UART.

---

## Communication Topology

```text
                              ┌─────────────────────────┐
                              │         Master          │
                              │           MPU           │
                              └────────────┬────────────┘
                                           │
                                      CAN Network
                                           │
                 ┌─────────────────────────┴───────────────────────┐
                 │                                                 │
      ┌──────────▼──────────┐                           ┌──────────▼──────────┐
      │       Slave A       │                           │       Slave B       │
      │         MCU         │                           │         MCU         │
      └──────────┬──────────┘                           └──────────┬──────────┘
                 │                                                 │
          I²C • SPI • UART                                  I²C • SPI • UART
                 │                                                 │
          Vehicle Sensors                                   Vehicle Sensors
```

---

## Communication Interfaces

| Interface | Purpose                                            | Scope    |
| --------- | -------------------------------------------------- | -------- |
| CAN       | Communication between Master and Slave modules     | System   |
| I²C       | Local communication with peripherals               | Local    |
| SPI       | High-speed peripheral communication                | Local    |
| UART      | Point-to-point communication with external devices | Local    |
| Ethernet  | Development and high-speed communication           | External |
| USB       | Programming, debugging and maintenance             | External |

---

## CAN Network

### CAN Purpose

The CAN bus is the primary communication channel of the Datalogger system.

### CAN Responsibilities

* Master ↔ Slave communication
* Sensor data transmission
* Configuration messages
* Diagnostics
* System status

### CAN Characteristics

* Multi-drop topology
* Differential signaling
* High reliability
* Fault tolerant
* Real-time communication

---

## I²C

### I²C Purpose

Provides communication with low-speed peripherals located on each module.

### I²C Typical Devices

* ADCs
* GPIO expanders
* I²C multiplexers
* Environmental sensors

---

## SPI

### SPI Purpose

Provides high-speed communication with local peripherals.

### SPI Typical Devices

* High-speed ADCs
* External memory
* Displays

---

## UART

### UART Purpose

Provides point-to-point communication with external devices.

### UART Typical Devices

* GNSS receivers
* IMUs
* Debug interfaces

---

## Ethernet

### Ethernet Purpose

Provides a high-speed interface for development and data transfer.

### Ethernet Typical Applications

* ROS 2 communication
* Software deployment
* Data download
* Remote diagnostics

---

## USB

### USB Purpose

Provides direct access for programming, debugging, and maintenance.

### USB Typical Applications

* Firmware upload
* Debugging
* Serial console
* Device configuration

---

## Communication Principles

The communication architecture follows these principles:

* Distributed data acquisition
* Standard communication interfaces
* Modular design
* Fault isolation
* Scalable architecture
* Reliable real-time communication
