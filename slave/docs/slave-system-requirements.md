# Datalogger Slave System Requirements

## Objective

Define the hardware and functional requirements for the Datalogger Slave board.

The goal is to establish the minimum required features for the first Slave PCB design, focusing on reliable sensor acquisition and communication while avoiding unnecessary complexity.

---

# Slave Overview

The Datalogger Slave is a distributed data acquisition module responsible for:

* Reading vehicle sensors
* Conditioning sensor signals
* Processing measurements locally
* Communicating acquired data through CAN
* Monitoring its own hardware status

The Slave should be designed as a robust acquisition module, not as a control unit.

---

# Functional Requirements

## Sensor Acquisition

The Slave must support multiple types of automotive sensors:

### Analog Inputs

Required:

* Measurement range compatible with automotive sensors
* Support for automotive voltage signals (0-12 V) through input conditioning circuits.
* Input protection
* Analog filtering before ADC

Examples:

* Pressure sensors
* Temperature sensors
* Potentiometers
* Position sensors

Initial target:

* 8 to 10 analog inputs

---

## Digital Inputs

Required:

* Reading external digital signals
* Protection against electrical noise
* Configurable input levels

Examples:

* Switches
* Digital sensors
* Status signals

Initial target:

* 4 to 8 digital inputs

---

## Frequency Inputs

Required for sensors that provide pulse signals.

Examples:

* Wheel speed sensors
* Hall sensors
* Encoders

Requirements:

* Timer capture support
* Frequency measurement
* Input filtering

---

# Outputs

Outputs are not required for the first Slave version.

The initial objective is data acquisition.

Not included:

* PWM outputs
* Actuator control
* High-current outputs

These can be considered in future revisions if required.

---

# Power System

## Input Supply

The Slave receives:

* 12 V vehicle supply

Required protections:

* Reverse polarity protection
* Input filtering
* Transient protection

---

## Power Rails

### 5 V Supply

Used for:

* External sensors
* Analog circuits

Requirements:

* Buck converter from 12 V
* Current protection
* Filtering

---

### 3.3 V Supply

Used for:

* Microcontroller
* Digital logic
* Communication circuits

Requirements:

* Stable regulation
* Filtering
* Decoupling

---

## Sensor Supply

The Slave should provide regulated sensor supply outputs.

Requirements:

- 5 V sensor supply
- Current protection
- Filtering
- Monitoring capability

Examples:

- Pressure sensors
- Potentiometers
- Temperature sensors

# Communication

# Interface Requirements

The Slave board must provide hardware interfaces for sensor acquisition, communication, debugging and future expansion.

| Interface | Purpose | Required | Notes |
|-----------|---------|----------|-------|
| CAN | Main communication interface | Yes | Communication with external modules, 500 kbps target |
| ADC | Analog sensor acquisition | Yes | Internal or external ADC, 0-5 V / 0-12 V conditioned inputs |
| GPIO | Digital inputs and status signals | Yes | Protected automotive digital inputs |
| Timer Input Capture | Frequency measurement | Yes | Wheel speed, Hall sensors, encoder signals |
| I2C | External sensor expansion | Yes | Low-speed sensors, ADCs, temperature sensors |
| SPI | High-speed peripherals expansion | Optional | External ADCs, memory, communication devices |
| UART | Debug and external communication | Yes | Firmware debugging and configuration |
| SWD/JTAG | Programming and debugging | Yes | MCU programming and real-time debugging |
| PWM | Output control | No | Not required in first revision |

## CAN Interface

The Slave communicates through CAN.

Requirements:

* CAN controller/interface
* CAN transceiver
* ESD protection
* Automotive noise robustness
* Termination resistor

Target:

* CAN 500 kbps

---

# Microcontroller Requirements

The MCU must support:

Required peripherals:

* ADC
* CAN
* Timers
* GPIO interrupts
* UART/SPI/I2C
* Debug interface
* Watchdog

---

# Diagnostics and Safety

The Slave should provide:

## Status Monitoring

Required indicators:

* Power status LED
* MCU status LED
* CAN communication/error LED

---

## Protection Features

Required:

* Power input protection
* Supply filtering
* ESD protection
* Watchdog monitoring
* Reset circuit

---

# PCB Requirements

The PCB should include:

* Clear separation between analog and digital sections
* Test points for critical signals
* Debug connector
* Expandable GPIO
* Reliable automotive connectors

---
