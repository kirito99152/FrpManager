# Technical Documentation: Centralized Proxy Management System (FrpManager)

## 1. Core Functionality and Purpose (Architectural Vision)

FrpManager is more than just a Graphical User Interface (Dashboard) for FRP configuration. It is designed as a **Secure Gateway Architecture Control Plane**, turning a Cloud VPS into a "Steel Shield" that protects backend servers and IoT devices located behind NAT or within Local Networks.

### Core Values:

*   **Internal Server Protection (Invisible Backend):** Application servers (Web, Database, Services) located behind NAT do not need to open any inbound ports to the Internet. They remain invisible to port scanners and immune to direct external attacks.
*   **Centralized Firewall:** Instead of configuring security on hundreds of individual servers, administrators focus resources on the central VPS Gateway. Here, tools like iptables, WAF, Rate Limiting, and SSL/TLS (Wildcard Domains) are deployed uniformly.
*   **NAT Traversal & Flexible Management:** Solves the challenge of exposing internal services (without public IPs) to the Internet via TCP, UDP, HTTP, and HTTPS protocols.
*   **Comprehensive Monitoring & Telemetry:** The Agent acts as an internal detective, monitoring hardware (CPU, RAM, Network), scanning listening ports, tracking systemd services, and streaming logs back to the center.

---

## 2. Operational Mechanism (Architecture & Operations)

The system operates on a **Client-Server** model using high-speed gRPC for communication, combined with the tunneling power of `FRP`.

### A. Server Node (Control Plane / Gateway VPS)
The coordination "brain" and Internet gateway. It runs:
*   **FrpManager Server (Go):** Handles gRPC connections from Agents, provides RESTful APIs & WebSockets for the Dashboard. Interacts with MySQL for metadata.
*   **FRP Server (frps):** Maintains tunnels and routes traffic from the Internet to internal machine tunnels.
*   **MySQL Database:** Stores all system metadata.

### B. Agent Node (Protected Servers behind NAT)
The target servers needing protection or external access. It runs:
*   **FrpManager Agent (Go):** Background application managing the node.
*   **FRP Client (frpc):** Process establishing the reverse tunnel to the VPS.

**Workflow:**
1.  **Connection Initialization (Outbound Only):** The Agent initiates an outbound gRPC connection to the Server (default Port 50051), bypassing NAT/Firewalls without port forwarding.
2.  **Registration & Licensing:** Agent sends hardware and network info to the Server. The Server generates a unique `Agent ID` and a secure `frpc.yaml` configuration.
3.  **Tunneling:** The Agent uses the assigned config to launch `frpc`, establishing a proxy tunnel to the `frps` on the central VPS.
4.  **Heartbeat & Telemetry:** The Agent continuously reports hardware metrics, open ports, service status, and real-time logs via gRPC.
5.  **Remote Control (Command Stream):** When an admin configures a new Proxy Rule on the Dashboard, the Server updates its DB and sends a command to the Agent to reload `frpc` instantly and transparently.

## 3. Hybrid Development Process (AI & Human)

FrpManager is a product of **AI-Assisted Engineering**:

1.  **AI Orchestration:** Multi-agent models were used to parallelize the development of independent modules.
2.  **Human Finalization:** The developer acts as the "Lead Architect," performing integration and production testing. Manual intervention ensures stability beyond the current reach of pure AI generation.
3.  **Continuous Improvement:** The system is maintained with ongoing support from Gemini CLI, accelerating feature deployment and reducing maintenance overhead.
