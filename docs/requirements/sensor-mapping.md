# Sensor Mapping

## Objective

Define the mapping between vehicle sensors, physical subsystems, and Datalogger Slave modules.

This document is used to define which sensors are connected to each Slave and where each Slave is physically located in the vehicle.

The mapping should consider:

* Physical sensor location
* Sensor type and interface
* Required acquisition rate
* Number of required inputs
* Wiring distance
* Slave hardware capabilities
* Communication requirements

## Sensor Mapping

| Subsystem        | Sensor              | Quantity | Interface        | Slave | Location          |
| ---------------- | ------------------- | -------: | ---------------- | ----- | ----------------- |
| Front Left       | Wheel Speed         |        1 | Frequency        | TBD   | Front Left Wheel  |
| Front Right      | Wheel Speed         |        1 | Frequency        | TBD   | Front Right Wheel |
| Rear Left        | Wheel Speed         |        1 | Frequency        | TBD   | Rear Left Wheel   |
| Rear Right       | Wheel Speed         |        1 | Frequency        | TBD   | Rear Right Wheel  |
| Steering         | Steering Angle      |        1 | Analog           | TBD   | Steering Column   |
| Front Suspension | Suspension Position |        2 | Analog           | TBD   | Front Suspension  |
| Rear Suspension  | Suspension Position |        2 | Analog           | TBD   | Rear Suspension   |
| Braking          | Brake Pressure      |        2 | Analog           | TBD   | Brake System      |
| Vehicle Dynamics | IMU                 |        1 | TBD              | TBD   | Vehicle Center    |
| Aerodynamics     | Pitot               |        1 | I2C / Digital    | TBD   | Vehicle Front     |

> The sensor list is preliminary and should be updated as the vehicle sensor requirements are defined.

## Slave Distribution

The Datalogger will use multiple Slave modules distributed throughout the vehicle.

Each Slave should be assigned to a physical subsystem where practical, reducing sensor wiring and simplifying local acquisition.

The final number and physical placement of Slaves will be determined based on:

* Sensor distribution
* Required I/O
* Wiring length
* Power distribution
* CAN bus topology
* Hardware constraints

### Slave 1

**Location:** TBD
**Subsystem:** TBD

| Sensor | Quantity | Interface |
| ------ | -------: | --------- |
| TBD    |      TBD | TBD       |

### Slave 2

**Location:** TBD
**Subsystem:** TBD

| Sensor | Quantity | Interface |
| ------ | -------: | --------- |
| TBD    |      TBD | TBD       |

## Mapping Rules

The following rules should be considered when assigning sensors to Slaves:

1. Sensors should preferably be connected to the physically closest Slave.
2. High-frequency signals should be considered when determining Slave placement.
3. Sensors requiring specialized interfaces should be assigned to Slaves with the required peripherals.
4. The number of sensors assigned to a Slave must remain within its available I/O and processing capacity.
5. Communication bandwidth must be considered when distributing high-rate signals.
6. Critical signals should have appropriate fault detection and communication handling.
7. The mapping should remain modular so that additional sensors or Slaves can be added without major architectural changes.

## Open Questions

* [ ] Define complete vehicle sensor list
* [ ] Define physical location of each sensor
* [ ] Define number of Slaves
* [ ] Define physical location of each Slave
* [ ] Assign each sensor to a Slave
* [ ] Verify Slave I/O capacity
* [ ] Verify CAN bandwidth requirements
* [ ] Verify power distribution requirements
