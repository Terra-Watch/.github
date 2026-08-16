# Jalri

Maritime safety and operations platform.

## Maritime Safety & Operations

Jalri provides operational tooling for maritime vessel monitoring, safety event management, and communication tracking. The system connects vessel-side BoatNodes to a shore-side dashboard through LoRa gateways and a REST backend.

## What Jalri Provides

- **Vessel status tracking** — register boats, monitor online/offline status through heartbeat communication
- **LoRa-based communication** — custom binary protocol (v3) with acknowledgement, retry, and duplicate detection
- **Gateway connectivity** — receive BoatNode packets over LoRa, forward events to the backend over HTTP
- **Operational dashboard** — fleet overview, vessel details, map, alerts, telemetry, history, and system status
- **Alert management** — SOS, system, and communication alerts with acknowledge/resolve workflow
- **Event history** — chronological records of heartbeats, alerts, registrations, and gateway events

## System

```text
BoatNode (ESP32-S3 + SX1278)
       │
       │ LoRa 433 MHz
       ▼
Gateway (ESP32-S3 + SX1278)
       │
       │ Wi-Fi / HTTP
       ▼
Backend (FastAPI + PostgreSQL)
       │
       │ REST API
       ▼
Dashboard (Next.js + React)
```

## Project Components

| Repository | Description |
|---|---|
| [jalari-node-firmware](https://github.com/RESQ-LoRa/jalari-node-firmware) | BoatNode embedded firmware (ESP32-S3, LoRa, protocol v3) |
| [jalri-gateway-firmware](https://github.com/RESQ-LoRa/jalri-gateway-firmware) | Gateway embedded firmware (LoRa RX, ACK TX, HTTP ingestion) |
| [website](https://github.com/RESQ-LoRa/website) | Frontend dashboard (Next.js) and backend API (FastAPI + PostgreSQL) |
| [jalari-ai](https://github.com/RESQ-LoRa/jalari-ai) | AI/ML capabilities (scaffolded) |
| [Documentation](https://github.com/RESQ-LoRa/Documentation) | Specifications, research papers, simulations |

## Project Status

Core software foundations are implemented across firmware, backend, and frontend. The BoatNode and Gateway firmware implement a custom LoRa protocol with heartbeat, acknowledgement, and backend ingestion. The backend provides 17 REST API endpoints with PostgreSQL persistence. The dashboard provides 10 operational pages.

Physical hardware integration and end-to-end RF validation remain pending.

## Documentation

Technical specifications, data contracts, and simulation analyses are available in the [Documentation](https://github.com/RESQ-LoRa/Documentation) repository.
