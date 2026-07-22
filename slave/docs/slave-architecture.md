# Datalogger Slave Architecture

| Field | Description |
|---|---|
| Module | Slave |
| Document Type | Architecture |
| Status | Draft |
| Version | 0.1 |

## Objective

Define the hardware and software architecture of the Datalogger Slave module.

This document describes the internal organization of the Slave, including power distribution, sensor acquisition, processing, communication interfaces, and expansion capabilities.

The Slave is designed as a distributed data acquisition module focused on reliable automotive sensor acquisition and CAN communication.

---

# System Overview

The Datalogger Slave is an embedded acquisition unit responsible for collecting data from multiple vehicle sensors, performing local signal processing, and transmitting measurements through the CAN network.

The Slave architecture is divided into the following main subsystems:

* Power Management
* Sensor Interface
* Signal Conditioning
* Processing Unit
* Communication Interface
* Diagnostics and Debug
* Expansion Interfaces

---

# High-Level Architecture

```
                 Vehicle Power
                      |
                    12V
                      |
              +----------------+
              | Power Management|
              +----------------+
                 |          |
                5V         3.3V
                 |          |
        +--------+----------+--------+
        |                         |
 Sensor Supply              Processing Unit
        |                         |
 Sensors                  +--------------+
        |                 | MCU           |
        |                 |               |
        |                 | ADC           |
        |                 | Timers        |
        |                 | CAN           |
        |                 +--------------+
        |
 Signal Conditioning
        |
        |
 CAN Network <---------- CAN Transceiver

```

---

# Power Architecture

## Input Stage

The Slave receives power from the vehicle electrical system.

Input:

* 12 V nominal supply

The input stage provides protection against automotive electrical conditions.

Required blocks:

* Reverse polarity protection
* Overcurrent protection
* Input filtering
* Transient voltage protection

---

## Voltage Regulation

The power system generates the required internal rails.

### 5 V Rail

Purpose:

* Sensor excitation
* Analog circuits
* External peripherals

Requirements:

* Buck conversion from 12 V
* Current protection
* Filtering

---

### 3.3 V Rail

Purpose:

* MCU
* Digital logic
* Communication circuits

Requirements:

* Low-noise regulation
* Decoupling capacitors
* Stable operation during load variation

---

# Sensor Interface Architecture

The Slave supports different sensor types through dedicated input stages.

---

## Analog Acquisition

Architecture:

```
Sensor
  |
Protection
  |
Filtering
  |
Voltage Conditioning
  |
ADC
  |
MCU
```

Supported sensors:

* Pressure sensors
* Temperature sensors
* Potentiometers
* Position sensors

Characteristics:

* Automotive voltage range support
* Noise filtering
* ADC-compatible voltage levels

---

## Digital Inputs

Architecture:

```
Digital Sensor
      |
Protection
      |
Filtering
      |
GPIO / Interrupt
      |
MCU
```

Used for:

* Switches
* Digital sensors
* Status signals

Requirements:

* Electrical protection
* Noise immunity
* Configurable input levels

---

## Frequency Inputs

Architecture:

```
Pulse Sensor
      |
Protection
      |
Signal Conditioning
      |
Timer Capture
      |
MCU
```

Used for:

* Wheel speed sensors
* Hall sensors
* Encoders

Requirements:

* Accurate timing measurement
* Interrupt/timer capture capability

---

# Processing Architecture

## Microcontroller

The MCU is responsible for:

* Sensor acquisition
* Data processing
* Communication management
* Diagnostics
* Fault monitoring

Required peripherals:

| Peripheral | Purpose               |
| ---------- | --------------------- |
| ADC        | Analog measurements   |
| Timers     | Frequency measurement |
| CAN        | Network communication |
| GPIO       | Digital signals       |
| UART       | Debug/configuration   |
| I2C        | Expansion             |
| SPI        | Expansion             |
| SWD        | Programming/debug     |

---

# Communication Architecture

## CAN Interface

CAN is the primary communication interface.

Architecture:

```
MCU CAN Peripheral
        |
        |
 CAN Transceiver
        |
        |
 CAN Bus
```

Responsibilities:

* Sensor data transmission
* Slave status messages
* Diagnostic information
* Configuration messages

Target:

* CAN 500 kbps

---

# Expansion Interfaces

The Slave provides additional interfaces for future hardware expansion.

## I2C

Purpose:

* External sensors
* Auxiliary ADCs
* Monitoring devices

Characteristics:

* Low-speed peripherals
* Multiple devices possible

---

## SPI

Purpose:

* High-speed peripherals
* External ADCs
* Memory devices

Characteristics:

* Higher bandwidth than I2C
* Short-distance communication

---

## UART

Purpose:

* Firmware debugging
* Configuration
* Development interface

---

# Diagnostics Architecture

The Slave must provide mechanisms for monitoring its own operation.

## Hardware Monitoring

Includes:

* Power status
* MCU activity
* CAN communication status

---

## Fault Detection

The system should monitor:

* Supply voltage
* Communication errors
* MCU failures
* Sensor acquisition faults

---

# Firmware Architecture

The firmware should be organized into independent layers.

```
Application Layer
        |
Sensor Management
        |
Hardware Abstraction Layer
        |
MCU Drivers
        |
Hardware
```

---

## Application Layer

Responsible for:

* Sensor scheduling
* Data formatting
* Communication management

---

## Sensor Layer

Responsible for:

* Sensor drivers
* Calibration
* Filtering
* Validation

---

## Hardware Abstraction Layer

Responsible for:

* ADC
* GPIO
* Timers
* Communication peripherals

---

# PCB Architecture Guidelines

The PCB should follow these principles:

## Analog / Digital Separation

Analog acquisition circuits should be separated from:

* Switching regulators
* CAN communication
* Digital clocks

---

## Protection Placement

Protection components should be placed close to connectors:

* TVS diodes
* Filtering components
* Input protection

---

## Debug Access

The PCB should include:

* SWD connector
* UART header
* Test points

---

# Design Principles

The Slave architecture follows these principles:

* Modular sensor acquisition
* Automotive robustness
* Expandability
* Simple debugging
* Minimal unnecessary hardware
* Clear separation between acquisition and processing

---

# Future Extensions

Possible future additions:

* External ADC modules
* Additional CAN channels
* More sensor interfaces
* Local data buffering
* Advanced diagnostics
