# 🤖 Minecraft 24/7 AFK Bot

<p align="center">
  <a href="README.md"><strong>🇺🇸 English (Current)</strong></a> &nbsp;|&nbsp; 
  <a href="README_VI.md"><strong>🇻🇳 Xem bản Tiếng Việt</strong></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-18+-green?logo=node.js&logoColor=white" alt="Node.js 18+" />
  <img src="https://img.shields.io/badge/Library-Mineflayer-blue" alt="Mineflayer" />
  <img src="https://img.shields.io/badge/Game-Minecraft_Java_Edition-388E3C?logo=minecraft&logoColor=white" alt="Minecraft" />
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT" />
</p>

<p align="center">
  <b>A lightweight, stable 24/7 Minecraft AFK bot built on Node.js and Mineflayer. Features auto-reconnect, AuthMe auto-login, anti-idle / anti-kick mechanisms, and 24/7 background deployment readiness.</b>
</p>

---

## 📖 Overview

**Minecraft 24/7 AFK Bot** is an automated assistant designed to keep chunks loaded for mob farms, crop farms, and in-game economy generation on Minecraft servers. The bot automatically manages connections, logs in via chat commands, and performs subtle movements to stay active indefinitely without getting disconnected by server anti-AFK plugins.

---

## ✨ Key Features

- 🔄 **Auto-Reconnect Engine**: Automatically attempts reconnection after a configurable delay whenever disconnected by server lag, restarts, or kicks.
- 🔐 **Auto-Login Support (AuthMe / NLogin)**: Automatically runs `/register` or `/login` upon joining cracked / offline-mode servers.
- 🏃 **Anti-AFK & Anti-Kick Mechanism**: Simulates periodic natural actions (jumping, looking around, swinging hand) at random intervals to bypass server idle detection.
- ⚙️ **JSON-Driven Configuration (`config.json`)**: Easily configure server IP, port, bot username, and password without modifying source code.
- ☁️ **Cloud & 24/7 Deployment Ready**: Preconfigured with `Procfile` for Heroku / Pterodactyl panels and easily managed via `PM2`.

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- [Node.js](https://nodejs.org/) (Version **16.x** or **18.x+**).
- A valid Minecraft server address (supports Java Edition servers).

---

### 2. Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/kingbone2006/afk-bot.git
   cd afk-bot
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

---

### 3. Configuration (`config.json`)

Create or edit `config.json` in the root directory:

```json
{
  "ip": "play.yourserver.net",
  "port": 25565,
  "name": "AFK_Farmer_Bot",
  "version": "1.20.1",
  "password": "your_secure_password"
}
```

| Field | Type | Description |
| :--- | :--- | :--- |
| `ip` | String | Server IP or domain name |
| `port` | Number | Server port (default `25565`) |
| `name` | String | In-game bot username |
| `version` | String | Minecraft server version (or `false` for auto-detect) |
| `password` | String | Password for `/login <password>` |

---

### 4. Running the Bot

Run the bot directly via Node:

```bash
node index.js
# Or
npm start
```

---

## 🔄 Running 24/7 in Background

### Using `PM2` (Recommended on VPS / Dedicated Server):
```bash
npm install -g pm2
pm2 start index.js --name "mc-afk-bot"
pm2 save
pm2 startup
```

To view live bot logs:
```bash
pm2 logs mc-afk-bot
```

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
