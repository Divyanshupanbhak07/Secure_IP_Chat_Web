# Secure IP-Based Temporary Chat Web Application

A full-stack, privacy-focused, real-time temporary chat web application designed for production-level software engineering standards and final-year CSE/IT academic project evaluation.

![Security Theme](https://img.shields.io/badge/Security-IP--Isolated-blue)
![Redis TTL](https://img.shields.io/badge/Storage-Redis%20TTL-emerald)
![WebRTC](https://img.shields.io/badge/P2P-WebRTC%20Audio%2FVideo-violet)
![TypeScript](https://img.shields.io/badge/Language-TypeScript-cyan)

---

## 🌟 Key Features

- 🔒 **Ephemeral Temporary Rooms**: Create chat sessions that automatically expire in 10, 30, or 60 minutes.
- ⚡ **Redis Native TTL Cleanup**: Zero permanent message persistence. Messages exist strictly in Redis volatile memory and are purged automatically upon TTL expiry.
- 🛡️ **Strict IP Isolation**: IP addresses are used **only** on the backend for rate limiting and abuse prevention. Raw IP addresses are **never** stored in message objects, logged, or rendered in client UIs.
- 🔑 **Cryptographic Token Authorization**: Unpredictable room IDs (`AB7X-K92P`) and cryptographically signed session tokens prevent room enumeration and unauthorized access.
- 💬 **Real-Time Communication**: Low-latency bidirectional messaging via Socket.IO with typing indicators and participant presence tracking.
- 📞 **WebRTC Voice & Video Calling**: Peer-to-Peer audio/video streaming integrated directly with Socket.IO signaling.
- 🛡️ **Comprehensive Security Controls**: Helmet security headers (CSP), strict CORS origins, Zod payload validation, and XSS auto-escaping.
- 🎓 **Academic Viva Prep Suite**: Dedicated interactive Viva Voce section containing 35+ Questions & Answers for project presentation and evaluation.

---

## 🛠️ Technology Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend** | React 18, Vite, TypeScript, Tailwind CSS, Lucide Icons, Socket.IO Client |
| **Backend** | Node.js, Express.js, TypeScript, Socket.IO Server |
| **Storage** | Redis (ioredis / automatic in-memory fallback for local dev) |
| **Security** | Helmet, CORS, express-rate-limit, Zod |
| **P2P Audio/Video**| WebRTC (RTCPeerConnection + Socket.IO signaling) |
| **Monorepo** | npm workspaces (`client`, `server`, `shared`) |

---

## 📁 Repository Structure

```text
secure-temporary-chat/
├── client/              # React 18 + Vite + TypeScript Frontend App
├── server/              # Node.js + Express + Socket.IO Backend Server
├── shared/              # Shared TypeScript DTOs, interfaces, and constants
├── docs/                # Architecture, API, Security, Database, Deployment & Viva docs
├── docker/              # Dockerfiles for Client & Server + Nginx config
├── docker-compose.yml   # Multi-container orchestration
├── .env.example         # Environment template
├── README.md            # Project documentation
└── package.json         # Monorepo root workspace config
```

---

## 🚀 Quick Start & Installation

### Prerequisites
- **Node.js**: v18.0 or higher
- **npm**: v9.0 or higher
- *(Optional)* **Redis / Docker**: Local Redis instance or Docker installed. If Redis is not running locally, the application automatically uses an in-memory mock fallback mode.

### 1. Clone & Install Dependencies
```bash
# Install all monorepo workspace dependencies (client, server, shared)
npm install
```

### 2. Configure Environment Variables
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```

### 3. Run Development Servers
Start both backend (Port 5000) and frontend (Port 5173) concurrently:
```bash
npm run dev
```

Visit the frontend client at: `http://localhost:5173`

---

## 🧪 Running Tests & Typechecks

```bash
# Run backend unit & security test suite
npm test

# Run TypeScript typechecks across all workspace packages
npm run typecheck

# Build production bundles
npm run build
```

---

## 🐳 Docker Deployment

To run the complete stack (Client, Server, Redis) in containerized isolation:
```bash
docker compose up --build
```

Access the containerized client at `http://localhost:5173`.

---

## 📚 Documentation Sitemap

Detailed documentation modules located in `/docs`:
- [`architecture.md`](file:///d:/project%2027/docs/architecture.md): System architecture and data flow diagrams.
- [`api.md`](file:///d:/project%2027/docs/api.md): REST endpoints and Socket.IO event reference.
- [`security.md`](file:///d:/project%2027/docs/security.md): Security threat model and mitigation matrix.
- [`database.md`](file:///d:/project%2027/docs/database.md): Redis key schema and TTL lifecycle.
- [`deployment.md`](file:///d:/project%2027/docs/deployment.md): Production HTTPS/WSS deployment guide.
- [`viva.md`](file:///d:/project%2027/docs/viva.md): 35+ Viva Voce questions & answers.

---

## 🎓 Demo Scenario for Viva Presentation

1. Open `http://localhost:5173` and click **Create Temporary Chat**.
2. Set display name (e.g. `Alice`) and duration preset (e.g. `10 Minutes`).
3. Copy generated Room Code (e.g. `AB7X-K92P`).
4. Open an Incognito browser window, navigate to **Join Existing Chat**, enter room code and name (`Bob`).
5. Send real-time messages and observe instant delivery, typing indicators, and presence updates.
6. Click the Video/Voice Call icon to demonstrate WebRTC P2P streaming.
7. Click **End Session** or allow timer expiration to demonstrate complete Redis data purge and socket termination.
