# 🌊 PalavariRaksha

**Engineering resilient maritime communication systems for small-scale fisheries.**

PalavariRaksha is an open engineering project focused on building an **offline-first maritime safety platform** for fishing communities. The system enables vessels to exchange emergency alerts, location updates, and operational messages even when conventional communication infrastructure is unavailable.

Instead of relying solely on cellular networks, PalavariRaksha combines embedded systems, LoRa mesh networking, distributed systems, and edge computing to create a fault-tolerant communication network suitable for coastal and offshore environments.

---

## The Problem

Small fishing vessels frequently operate beyond reliable cellular coverage. During emergencies such as:

* Man Overboard (MOB)
* Engine failure
* Extreme weather
* Medical emergencies
* Loss of communication

obtaining timely assistance becomes difficult.

PalavariRaksha explores how low-power embedded systems and decentralized networking can improve situational awareness and emergency response in these environments.

---

## Engineering Principles

This organization follows an engineering-first workflow.

```text
Research
    ↓
System Design
    ↓
Analysis & Validation
    ↓
Prototype Development
    ↓
Hardware Integration
    ↓
Field Testing
    ↓
Documentation
```

Every design decision should be supported by analysis, experiments, or implementation—not assumptions.

---

## Organization

| Repository     | Purpose                                                               |
| -------------- | --------------------------------------------------------------------- |
| `docs`         | System design documents, architecture, specifications and reports     |
| `boatnode`     | Vessel communication node firmware                                    |
| `wristnode`    | Crew wearable safety device                                           |
| `shorestation` | Shore gateway and monitoring station                                  |
| `simulations`  | Network analysis, TDMA scheduling, routing experiments and evaluation |
| `hardware`     | Schematics, PCB files, BOM and mechanical designs                     |
| `mobile-app`   | Offline crew interface                                                |
| `backend`      | Cloud services and APIs                                               |
| `dashboard`    | Shore monitoring dashboard                                            |

---

## Technical Areas

* Embedded Systems
* LoRa Communication
* Mesh Networking
* Delay Tolerant Networking (DTN)
* Routing Algorithms
* Real-Time Systems
* Wireless Communication
* Edge Computing
* Maritime Safety Systems

---

## Repository Standards

Every repository should contain:

* Design documentation
* Source code
* Experiment results
* Test reports
* Issues and milestones
* Version history

Documentation evolves alongside implementation to ensure that design decisions remain traceable throughout the project lifecycle.

---

## About

PalavariRaksha is developed as part of a B.Tech final-year engineering project at **Amrita Vishwa Vidyapeetham, Ettimadai**.

This organization serves as the central workspace for research, development, experimentation, documentation, and hardware integration.
