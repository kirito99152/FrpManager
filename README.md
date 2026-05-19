# 🚀 FrpManager: FRP Centralized Management System

**FrpManager** is a centralized management system for **Fast Reverse Proxy (FRP) v0.68.0**. It provides a powerful Control Plane to monitor, control, and establish tunnels for thousands of remote servers.

---

## 🤖 Hybrid Development Journey (AI & Human)

This project is a testament to the powerful combination of **AI Agents** and **Human** technical refinement:

*   **80% System Scaffolding:** Initialized by 4 AI Agents (Gemini CLI) working in parallel, maximizing the speed of building gRPC, REST API, Dashboard, and DevOps within a very short timeframe.
*   **20% Refinement & Production-Ready:** Manually refined by the Human Architect through intensive testing with a single Gemini CLI. This phase focused on:
    *   Optimizing gRPC and WebSocket connection stability.
    *   Handling network edge cases and disaster recovery.
    *   Ensuring enterprise-grade security and tunnel performance.

---

## ✨ Key Features

*   **Real-time Monitoring:** Server health charts (CPU, RAM, Network) updated continuously via WebSocket.
*   **Smart Port Scanner:** Automatically detects open ports and identifies services on the client machine.
*   **Log Streaming:** Monitor remote system logs in real-time (standard `tail -f` behavior).
*   **FRP v0.68.0 Integration:** Full tunnel management using YAML configuration, supporting HTTP/TCP/UDP.
*   **Wildcard Subdomain Support:** Supports creating HTTP proxies with wildcard domains and uniqueness checks.
*   **Enterprise Security:** JWT Authentication and network isolation using Docker Networks.

---

## 🏗️ Architecture & Tech Stack

*   **Protocols:** gRPC (Client-Server), WebSocket (Real-time Stats).
*   **Backend:** Golang (Gin), MySQL.
*   **Frontend:** React, Vite, Tailwind CSS, Recharts.
*   **Infrastructure:** Docker Compose, Nginx Reverse Proxy, Systemd (Agent Watchdog).

---

## 📋 System Requirements
*   **Go:** v1.22+
*   **Node.js:** v20.x+
*   **MySQL:** v8.0+
*   **FRP:** v0.68.0
    *   Uses `.yaml` configuration format.
    *   Requires both `frps` (server) and `frpc` (agent) to be on version 0.68.0 for best compatibility.

---

## 🚀 Deployment Guide

### 1. Server Deployment (Control Plane)
The project supports two main deployment methods.

#### Method 1: Installation Script (Recommended)
The fastest way to build and install the system directly on the host using `systemd`.

```bash
# 1. Install full environment (Go, Node, MySQL, FRPS)
bash setup.sh

# 2. Run update and build script
bash scripts/update-server.sh
```

#### Method 2: Docker Deployment
For isolated container environments:

```bash
# Launch the full stack (Server + MySQL)
docker-compose up -d --build
```
Note: Edit environment variables in `.env` or `docker-compose.yml` before running.

### 2. Client Agent Deployment
On target nodes, run the automated installation script:
```bash
bash scripts/install-agent.sh --server <YOUR_SERVER_IP>:50051
```

### 3. Usage:
*   **Dashboard:** View Online/Offline status of all Nodes.
*   **Logs:** View live log streams from Agent services.
*   **Proxy Mapping:** Set up Domain and Port mappings to internal machines via FRP.

---

## 📚 Documentation
For deeper insights, please refer to:
*   [Technical Architecture Docs](FrpManager_Documentation.md)
*   [Professional User Guide](GUIDE.md)

---

## 🧪 Testing Strategy
The system has been tested against:
1.  **Stress Test:** Simulated 100+ Agents sending Heartbeats simultaneously.
2.  **Security Test:** Verified unauthorized access blocking without valid JWT Tokens.
3.  **Stability Test:** Agent auto-restarts on Panic or network loss.

**This project was completed under the supervision of the Lead Architect.**
