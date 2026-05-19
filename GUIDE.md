# FrpManager - Ultimate Professional Guide

Welcome to the professional centralized Proxy management system. This is the production-ready version, optimized through hybrid development between AI and a Human Architect.

## 📦 1. Server Deployment (Docker)

Use Docker Compose to launch the entire infrastructure with a secure, isolated network.

```bash
docker-compose -f deploy/docker/docker-compose.yml up -d --build
```

- **Dashboard:** `http://your-server-ip`
- **API Server:** `http://your-server-ip:8081`
- **FRPS:** Port 7000 (Tunnel), 7500 (Dashboard).

## 🛡️ 2. Security & Authentication (JWT)

Access the Dashboard and log in using default credentials:
- **User:** `admin`
- **Pass:** `admin123` (Change immediately in the **Profile** section).

The system uses JWT Tokens to protect all API requests and WebSocket connections. If the token expires, you will be automatically redirected to the login page.

## 📟 3. Remote Terminal (Shell Console)

You can execute commands directly on Agents via the Dashboard:
1. Go to the **Terminal** section in the Sidebar.
2. Select the target Agent from the list.
3. Enter commands (e.g., `ls`, `df -h`, `netstat`) and press Enter.
*Note: Only safe commands are allowed.*

## 📜 4. Log Monitoring (Log Viewer)

The **Logs** section allows you to view real-time log streams from all Agents:
- Filter by **Severity** (Info, Warning, Error).
- Search by log content.
- Auto-scroll to the latest data.

## ⚙️ 5. Webhook Configuration (Alerting)

Go to the **Settings** section to configure automated notifications:
- **Telegram:** Enter Bot Token and Chat ID.
- **Discord:** Enter Webhook URL.
The system will send alerts when an Agent goes offline or resource issues occur.

## 🚀 6. Installing New Agents

Run the following command on a client node for automated installation:
```bash
curl -sSL https://raw.githubusercontent.com/kirito99152/FrpManager/main/scripts/install-agent.sh | sudo bash
```
After installation, the Agent will automatically start with the system via **systemd**.

---
*Enjoy your experience with FrpManager!*
