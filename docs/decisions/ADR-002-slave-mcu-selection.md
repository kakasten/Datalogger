# ADR-002: Slave MCU Selection

## Status

Accepted

## Context

The Datalogger Slave requires a microcontroller capable of handling:

- Sensor acquisition
- CAN FD communication
- Timer-based frequency measurement
- I2C peripherals
- ADC acquisition
- Real-time firmware execution
- Debugging through SWD

The MCU must also provide sufficient peripheral resources while keeping
the hardware complexity and cost reasonable.

## Decision

The STM32G431C8T6T**R** will be used as the main microcontroller of the
Datalogger Slave. The complete selected ordering code is
**STM32G431C8T6TR**.

## Alternatives Considered

### STM32G431C8T6TR

- CAN FD peripheral
- Multiple timers
- ADC peripherals
- I2C interfaces
- SWD debugging
- Suitable performance for the required acquisition rates

### STM32F103

Rejected because it does not provide CAN FD and has fewer resources
available for the planned architecture.

## Consequences

### Positive

- Native CAN FD support
- Sufficient timer resources
- Suitable ADC and I2C peripherals
- Good debugging support
- Keeps the Slave architecture relatively simple

### Negative

- Firmware becomes tied to the STM32G4 family
- Requires STM32-specific development tools and HAL/LL dependencies