# Repository Organization

## Objective

Define the repository structure of the Datalogger project and describe the purpose of each directory.

---

## Repository Structure

```text
amp-datalogger/
│
├── README.md
│
├── docs/
│   ├── requirements/
│   │   ├── system.md
│   │   ├── master.md
│   │   ├── slave.md
│   │   └── ate.md
│   │
│   ├── architecture/
│   │   ├── 01-system-overview.md
│   │   ├── 02-network.md
│   │   ├── 03-power-architecture.md
│   │   ├── 04-software-architecture.md
│   │   ├── 05-hardware-architecture.md
│   │   └── 06-repository-structure.md
│   │
│   ├── interfaces/
│   │   ├── can.md
│   │   ├── i2c.md
│   │   ├── spi.md
│   │   └── uart.md
│   │
│   ├── decisions/
│   │   ├── ADR-0001-...
│   │   └── ADR-0002-...
│   │
│   └── diagrams/
│
├── commons/
│   └── hardware/
│       └── kicad/
│
├── master/
│
├── slave/
│
└── ate/
```

---

## Directory Description

### README.md

Entry point of the repository. Provides a high-level description of the project and links to the available documentation.

---

### docs/

Contains all engineering documentation related to the project.

---

### docs/requirements/

System and subsystem requirements.

Examples:

- System requirements
- Master requirements
- Slave requirements
- ATE requirements

---

### docs/architecture/

High-level system architecture documentation.

Includes:

- System overview
- Hardware architecture
- Software architecture
- Communication architecture
- Power architecture
- Repository organization

---

### docs/interfaces/

Defines communication interfaces used throughout the project.

Examples:

- CAN
- I²C
- SPI
- UART

Each document specifies the interface purpose, configuration, and design guidelines.

---

### docs/decisions/

Architecture Decision Records (ADRs).

Each ADR documents an important engineering decision, including its motivation, alternatives, and consequences.

---

### docs/diagrams/

Stores architecture and system diagrams in editable and exported formats.

Examples:

- Draw.io
- SVG
- PNG
- PDF

---

### commons/

Contains resources shared across multiple projects in the repository.

This directory is intended for reusable assets that are not specific to a single module.

Current contents:

- Shared KiCad symbol libraries
- Shared KiCad footprint libraries
- KiCad project templates

As the project evolves, additional shared resources may be added while keeping them independent from the Master, Slave, and ATE projects.

---

### master/

Contains all files related to the Master module.

Typical contents include:

- Hardware
- Firmware
- Documentation
- Manufacturing files

---

### slave/

Contains all files related to the Slave module.

Typical contents include:

- Hardware
- Firmware
- Documentation
- Manufacturing files

---

### ate/

Contains the Automated Test Equipment (ATE) project.

Typical contents include:

- Test hardware
- Test software
- Test procedures
- Validation reports

---

## Organization Principles

The repository organization follows these principles:

- Separation of concerns
- Modular development
- Independent documentation
- Version-controlled engineering artifacts
- Easy navigation and maintenance
