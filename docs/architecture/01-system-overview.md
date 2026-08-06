# System Overview

## Purpose

The Datalogger system is a modular data acquisition platform designed for Formula SAE vehicles. It acquires data from vehicle sensors through distributed acquisition modules (Slaves), transmits the data over a CAN network, and centralizes logging, processing, and telemetry in the Master module.

---

## System Objectives

* Acquire data from analog, digital, frequency, and CAN sensors.
* Provide a modular and scalable hardware architecture.
* Minimize wiring complexity by distributing sensor acquisition.
* Ensure reliable communication between all modules.
* Store synchronized vehicle data for post-processing.
* Support real-time telemetry and diagnostics.

---

## System Components

The system is composed of two primary modules:

* Master
* Slave

Each Slave is responsible for acquiring sensors located near its installation point, while the Master is responsible for coordinating the system, logging data, and interfacing with external devices.

---

## High-Level Architecture

```text
                              ┌────────────────────────────┐
                              │           Master           │
                              │            MPU             │
                              │     ROS 2 • Data Logging   │
                              │         Telemetry          │
                              └────────────┬───────────────┘
                                           │
                                       CAN Network
                                           │
                 ┌─────────────────────────┴───────────────────────┐
                 │                                                 │
      ┌──────────▼──────────┐                           ┌──────────▼──────────┐
      │       Slave A       │                           │       Slave B       │
      │         MCU         │                           │         MCU         │
      │ Analog • Digital IO │                           │ Analog • Digital IO │
      └──────────┬──────────┘                           └──────────┬──────────┘
                 │                                                 │
          Vehicle Sensors                                   Vehicle Sensors
```

---

## Data Flow

1. Sensors generate electrical signals.
2. Slave modules acquire and condition the signals.
3. Measurements are transmitted over the CAN bus.
4. The Master receives all messages.
5. Data is logged and optionally transmitted via telemetry.

---

## Main Features

* Distributed acquisition
* CAN-based communication
* Modular hardware
* ROS 2 software architecture
* Local data logging
* Telemetry support
* Fault isolation
* Expandable architecture
