# RustDesk Docker Deployment

![Last commit](https://img.shields.io/github/last-commit/panhavad/rustdesk-doker-deployment) [![Release](https://img.shields.io/github/v/release/panhavad/rustdesk-doker-deployment?include_prereleases)](https://github.com/panhavad/rustdesk-doker-deployment/releases/latest)

Run your own **self-hosted RustDesk server** with Docker Compose. It starts the **hbbs** (ID / rendezvous) and **hbbr** (relay) services so your remote-desktop traffic stays on your own server.

![System snapshot](docs/snapshot.svg)

## Features

- hbbs + hbbr in one compose file
- Persistent keys in `./data`
- Host networking for easy NAT traversal
- Auto restart

## How it works

```mermaid
flowchart LR
    A["RustDesk client A"] -->|"ID lookup 21116"| S["hbbs"]
    B["RustDesk client B"] -->|"ID lookup"| S
    S -->|"direct P2P if possible"| A
    A -->|"fallback relay 21117"| R["hbbr"]
    R --> B
```

## Getting started

```bash
docker compose up -d
cat data/id_ed25519.pub   # public key for clients
```
In the RustDesk client set **ID server** to your host and paste the key.

## Download

Grab the packaged source from the [latest release](https://github.com/panhavad/rustdesk-doker-deployment/releases/latest).

## Tech stack

- Docker Compose
- RustDesk server

## Project structure

```text
rustdesk-doker-deployment/
├── docs/
├── compose.yaml
└── README.md
```
