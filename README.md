# DPI-Engine
High-Performance Deep Packet Inspection (DPI) Engine built in C++ for network traffic analysis, application identification, and packet filtering.

## Overview
DPI-Engine is a multi-threaded packet inspection system capable of analyzing PCAP files, identifying applications using TLS SNI extraction, tracking flows using Five-Tuple classification, and applying custom blocking rules.

The project demonstrates:
- Network protocol parsing
- TLS SNI extraction
- Stateful flow tracking
- Multi-threaded packet processing
- Traffic classification
- Rule-based filtering

---

## Features

- Deep Packet Inspection (DPI)
- TLS SNI Extraction
- HTTP Host Extraction
- Flow Tracking using Five-Tuple
- Multi-threaded Processing Architecture
- Rule-based Blocking System
- PCAP File Processing
- Traffic Classification
- Application Detection
- Detailed Processing Reports

---

## Supported Application Detection

- YouTube
- Facebook
- Google
- DNS
- HTTPS
- HTTP

Additional signatures can easily be added.

---

## Project Architecture

```text
                ┌─────────────────┐
                │  Reader Thread  │
                └────────┬────────┘
                         │
          ┌──────────────┴──────────────┐
          ▼                             ▼
   ┌──────────────┐             ┌──────────────┐
   │ LoadBalancer │             │ LoadBalancer │
   └──────┬───────┘             └──────┬───────┘
          ▼                             ▼
   ┌──────────────┐             ┌──────────────┐
   │  Fast Path   │             │  Fast Path   │
   │   Threads    │             │   Threads    │
   └──────┬───────┘             └──────┬───────┘
          └──────────────┬─────────────┘
                         ▼
                 ┌──────────────┐
                 │ Output Writer│
                 └──────────────┘
```

---

## Tech Stack

- C++17
- Multi-threading
- TCP/IP Networking
- PCAP Parsing
- TLS Inspection
- STL Containers
- Mutex & Condition Variables

---

## File Structure

```text
packet_analyzer/
│
├── include/
│   ├── pcap_reader.h
│   ├── packet_parser.h
│   ├── sni_extractor.h
│   ├── types.h
│   └── dpi_engine.h
│
├── src/
│   ├── pcap_reader.cpp
│   ├── packet_parser.cpp
│   ├── sni_extractor.cpp
│   ├── main_working.cpp
│   └── dpi_mt.cpp
│
├── generate_test_pcap.py
├── test_dpi.pcap
└── README.md
```

---

## How It Works

1. Read packets from PCAP file
2. Parse Ethernet/IP/TCP/UDP headers
3. Create Five-Tuple flow
4. Extract TLS SNI or HTTP Host
5. Classify application traffic
6. Apply filtering rules
7. Forward or drop packets
8. Generate analytics report

---

## Building the Project

### Linux / macOS

### Simple Version

```bash
g++ -std=c++17 -O2 -I include -o dpi_simple \
src/main_working.cpp \
src/pcap_reader.cpp \
src/packet_parser.cpp \
src/sni_extractor.cpp \
src/types.cpp
```

### Multi-threaded Version

```bash
g++ -std=c++17 -pthread -O2 -I include -o dpi_engine \
src/dpi_mt.cpp \
src/pcap_reader.cpp \
src/packet_parser.cpp \
src/sni_extractor.cpp \
src/types.cpp
```

---

## Running the Engine

### Basic Usage

```bash
./dpi_engine test_dpi.pcap output.pcap
```

### Block Applications

```bash
./dpi_engine test_dpi.pcap output.pcap \
--block-app YouTube \
--block-app Facebook
```

### Configure Threads

```bash
./dpi_engine input.pcap output.pcap --lbs 4 --fps 4
```

---

## Sample Output

```text
[Reader] Processing packets...
[Reader] Done reading 77 packets

Forwarded: 69
Dropped: 8

Detected Applications:
- YouTube
- Facebook
- Google
- HTTPS
```

---

## Key Concepts Used

- Deep Packet Inspection
- TLS Handshake Analysis
- SNI Extraction
- Producer-Consumer Pattern
- Thread-safe Queues
- Flow-based Filtering
- Consistent Hashing
- Multi-threaded Design

---

## Future Improvements

- Real-time packet capture
- QUIC / HTTP3 support
- Web dashboard
- Threat detection
- Packet visualization
- AI-based traffic classification
- Docker deployment

---

## Educational Purpose

This project is designed for:
- Computer Networks
- Cybersecurity
- System Programming
- High-performance Networking
- Operating Systems
- Multithreading Concepts

---

## Author

Kaushal Kaushik
