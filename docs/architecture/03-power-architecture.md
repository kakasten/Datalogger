# Power Architecture

## Objective

Describe the power architecture of the Datalogger system, including power input, distribution, regulation, protection, and the main power domains used by the hardware.

---

## Overview

The Datalogger system is powered from the vehicle electrical system. The incoming vehicle supply is distributed through protected and regulated power stages to provide the voltage levels required by the Master, Slave modules, sensors, and peripheral devices.

The power architecture separates vehicle power, sensor power, and sensitive electronic power domains to improve system reliability and reduce the impact of electrical noise.

---

## System Power Architecture

```text
                         Vehicle Power
                              │
                              │
                       ┌──────▼──────┐
                       │    Input    │
                       │ Protection  │
                       └──────┬──────┘
                              │
                         Power Input
                              │
              ┌───────────────┴───────────────┐
              │                               │
       ┌──────▼──────┐                 ┌──────▼──────┐
       │    Master   │                 │    Slave    │
       │ Power Stage │                 │ Power Stage │
       └──────┬──────┘                 └──────┬──────┘
              │                               │
       ┌──────┴──────┐                ┌───────┴────────┐
       │             │                │                │
    Digital       Peripheral       Digital          Sensors
    Power           Power           Power            Power
       │             │                │                │
      MPU        Interfaces           MCU        Analog / Digital
```

---

## Power Domains

The system is divided into several power domains according to the requirements of each subsystem.

| Power Domain        | Purpose                   | Typical Loads                           |
| ------------------- | ------------------------- | --------------------------------------- |
| Vehicle Input       | Primary system supply     | Master and Slave modules                |
| Digital Power       | Digital electronics       | MPU, MCU, digital ICs                   |
| Analog Power        | Low-noise analog circuits | ADCs, signal conditioning               |
| Sensor Power        | Vehicle sensors           | Pressure, temperature, position sensors |
| Communication Power | Communication interfaces  | CAN, Ethernet, USB                      |
| Peripheral Power    | Local peripherals         | Displays, memory, external devices      |

---

## Input Power

The vehicle electrical system provides the primary power source for the Datalogger.

The input power stage is responsible for protecting the electronics against electrical disturbances present in the vehicle power network.

Typical protection functions include:

* Reverse polarity protection
* Overvoltage protection
* Transient protection
* Overcurrent protection
* Input filtering

The exact protection implementation is defined in the corresponding hardware design documentation.

---

## Power Regulation

The vehicle input voltage is converted into regulated voltage rails required by the system.

```text
Vehicle Input
     │
     ▼
Input Protection
     │
     ▼
Voltage Conversion
     │
     ├──────────► Digital Power
     │
     ├──────────► Analog Power
     │
     └──────────► Sensor Power
```

Voltage conversion stages are selected according to the required output voltage, current capability, efficiency, thermal performance, and electrical noise requirements.

---

## Master Power

The Master contains its own power regulation and distribution stages.

The Master power system provides regulated power to:

* MPU
* Storage
* CAN interface
* Ethernet interface
* USB interface
* Other local peripherals

The Master power architecture is designed to support the computational and communication requirements of the central processing module.

---

## Slave Power

Each Slave contains local power regulation and distribution.

The Slave power system provides power to:

* MCU
* ADCs
* Signal conditioning circuits
* Communication interfaces
* Vehicle sensors
* Local peripherals

Local regulation allows each Slave to operate as an independent acquisition module and reduces the need to distribute multiple regulated voltages throughout the vehicle.

---

## Sensor Power

Sensor power is distributed locally by the Slave modules whenever practical.

This approach reduces wiring complexity and allows sensor power requirements to be managed independently for each acquisition module.

Sensor power may include dedicated voltage rails for different sensor types and electrical requirements.

---

## Analog and Digital Power

Analog and digital circuits are treated as separate power domains where required.

Analog power is intended for noise-sensitive circuits such as:

* ADCs
* Operational amplifiers
* Analog signal conditioning
* Precision references

Digital power is used for:

* MCUs
* MPUs
* Digital communication interfaces
* Logic circuits

The separation of these domains helps reduce digital switching noise coupling into analog measurements.

---

## Power Distribution Principles

The power architecture follows these principles:

* Protected vehicle power input
* Local voltage regulation
* Separation of analog and digital power domains
* Dedicated sensor power distribution
* Modular power architecture
* Protection against automotive electrical disturbances
* Adequate current and thermal margins
* Minimized noise coupling
* Independent operation of acquisition modules

---

## Detailed Power Design

Detailed information about regulators, protection devices, voltage rails, current requirements, component selection, and PCB power routing is documented in the corresponding Master and Slave hardware documentation.
