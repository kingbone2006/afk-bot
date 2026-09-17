# 🤖 Minecraft 24/7 AFK Bot

<p align="center">
  <a href="README.md"><strong>🇺🇸 English</strong></a> &nbsp;|&nbsp; 
  <a href="README_VI.md"><strong>🇻🇳 Tiếng Việt (Hiện tại)</strong></a>
</p>


<p align="center">
  <img src="https://img.shields.io/badge/Node.js-16%2B-green.svg?style=for-the-badge&logo=node.js" alt="Node.js" />
  <img src="https://img.shields.io/badge/Library-Mineflayer-blue.svg?style=for-the-badge" alt="Mineflayer" />
  <img src="https://img.shields.io/badge/Minecraft-Java%20Edition-red.svg?style=for-the-badge&logo=minecraft" alt="Minecraft" />
  <img src="https://img.shields.io/badge/Deployment-VPS%20%7C%20Heroku%20%7C%20Replit-orange.svg?style=for-the-badge" alt="Deploy" />
</p>

A lightweight, automated 24/7 **AFK Bot** for Minecraft Java Edition servers built with [Mineflayer](https://github.com/PrismarineJS/mineflayer). Designed to keep chunks loaded for mob grinders, automatic farms, and maintain server activity without getting kicked for being idle.

---

## 📑 Mục lục / Table of Contents
- [Tính năng chính / Key Features](#-tính-năng-chính--key-features)
- [Yêu cầu hệ thống / Requirements](#-yêu-cầu-hệ-thống--requirements)
- [Cài đặt & Khởi chạy / Installation & Setup](#-cài-đặt--khởi-chạy--installation--setup)
- [Cấu hình / Configuration Guide](#-cấu-hình--configuration-guide)
- [Chạy ngầm 24/7 bằng PM2 / 24/7 with PM2](#-chạy-ngầm-247-bằng-pm2--247-with-pm2)
- [Triển khai lên Cloud / Cloud Deployment](#-triển-khai-lên-cloud--cloud-deployment)
- [Lưu ý / Disclaimer](#-lưu-ý--disclaimer)

---

## 🌟 Tính năng chính / Key Features

- **🔄 Chống Kick AFK thông minh (Anti-AFK Engine)**:
  - Tự động di chuyển ngẫu nhiên theo 4 hướng (`forward`, `back`, `left`, `right`).
  - Xoay góc nhìn (Yaw & Pitch) ngẫu nhiên mô phỏng hành vi của người chơi thật.
  - Tương tác / sử dụng vật phẩm định kỳ (`activateItem`).
- **🔐 Hỗ trợ máy chủ Offline / Crack (AuthMe Support)**:
  - Tự động gửi lệnh đăng ký (`/register`) và đăng nhập (`/login`) khi vào server.
- **💀 Tự động hồi sinh (Auto-Respawn)**:
  - Lập tức hồi sinh và tiếp tục hoạt động nếu bot bị quái vật hoặc người chơi khác hạ gục.
- **☀️ Bỏ qua ban đêm (Auto-Night Skip)**:
  - Tùy chọn tự động gửi lệnh `/time set day` khi trời tối (dành cho server cho phép).
- **☁️ Sẵn sàng chạy Cloud 24/7**:
  - Tích hợp sẵn `Procfile` để deploy dễ dàng lên Heroku, Render, Replit, VPS.

---

## 💻 Yêu cầu hệ thống / Requirements

- **Node.js**: Phiên bản `14.x`, `16.x` hoặc mới hơn (Khuyên dùng Node.js 18 LTS).
- **npm**: Đi kèm với Node.js.
- **Minecraft Server**: Bất kỳ máy chủ Minecraft Java Edition nào (hỗ trợ cả Online/Offline-mode).

---

## 🚀 Cài đặt & Khởi chạy / Installation & Setup

### Bước 1: Clone mã nguồn về máy hoặc VPS
```bash
git clone https://github.com/kingbone2006/afk-bot.git
cd afk-bot
```

### Bước 2: Cài đặt các thư viện cần thiết
```bash
npm install
```

### Bước 3: Cấu hình bot
Mở file `config.json` bằng trình soạn thảo và chỉnh sửa thông tin server của bạn:

```json
{
    "ip": "play.yourserver.com",
    "port": 25565,
    "name": "AFK_Bot_Name",
    "auto-night-skip": "false",
    "login-enabled": "true",
    "register-cmd": "/register matkhau123 matkhau123",
    "login-cmd": "/login matkhau123"
}
```

### Bước 4: Khởi động bot
```bash
npm start
# hoặc
node index.js
```

---

## ⚙️ Hướng dẫn cấu hình (`config.json`)

| Tham số / Parameter | Kiểu / Type | Ý nghĩa / Description |
| :--- | :--- | :--- |
| `ip` | String | Địa chỉ IP hoặc tên miền máy chủ Minecraft (VD: `mc.hypixel.net`, `localhost`). |
| `port` | Number | Cổng kết nối của server (mặc định là `25565`). |
| `name` | String | Tên nhân vật (In-game name) của bot khi xuất hiện trong game. |
| `auto-night-skip` | String | `"true"` để tự động chạy `/time set day` khi đêm xuống; `"false"` để tắt. |
| `login-enabled` | String | `"true"` nếu server yêu cầu đăng nhập bằng AuthMe (`/login`); `"false"` nếu là server Premium/Online-mode. |
| `register-cmd` | String | Cú pháp đăng ký gửi tới server (VD: `/register matkhau matkhau`). |
| `login-cmd` | String | Cú pháp đăng nhập gửi tới server (VD: `/login matkhau`). |

---

## ⏱️ Chạy ngầm 24/7 bằng PM2 (Khuyên dùng cho VPS)

Để bot tự động hoạt động liên tục ngay cả khi bạn tắt cửa sổ SSH terminal, hãy sử dụng **PM2**:

```bash
# 1. Cài đặt PM2 toàn cục
npm install -g pm2

# 2. Khởi động bot với PM2
pm2 start index.js --name "minecraft-afk-bot"

# 3. Cài đặt tự khởi động cùng hệ thống khi VPS reboot
pm2 startup
pm2 save

# 4. Xem nhật ký hoạt động / log của bot
pm2 logs minecraft-afk-bot

# 5. Dừng hoặc khởi động lại bot
pm2 stop minecraft-afk-bot
pm2 restart minecraft-afk-bot
```

---

## ☁️ Triển khai lên Cloud (Heroku / Replit / Render)

Dự án đã có sẵn file `Procfile` chuẩn:
```text
worker: node index.js
```

1. Đẩy code lên GitHub repository của bạn.
2. Kết nối repo với dịch vụ Cloud (Heroku, Render, Railway, Replit).
3. Cấu hình biến môi trường hoặc chỉnh sửa file `config.json` tương ứng.
4. Bật dyno / worker để bot chạy 24/7 không cần bật máy tính cá nhân.

---

## 📄 Lưu ý / Disclaimer

- Vui lòng kiểm tra kỹ nội quy (Rules) của máy chủ trước khi sử dụng bot AFK để tránh bị xử phạt (ban) nếu máy chủ nghiêm cấm bot tự động.
- Dự án được phát triển nhằm mục đích phục vụ máy chủ cá nhân, kiểm thử chunk farm và học tập lập trình với thư viện Mineflayer.
