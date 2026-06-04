---
title: Deploy a Personal Photo Album Accessible Anytime, Anywhere on Your Personal Computer
description: 个人电脑上部署一台随时随地可访问的私人相册
date: '2025-11-24'
categories:
    - Tools
tags:
    - Tools
---

# Deploy a Personal Photo Album Accessible Anytime, Anywhere on Your Personal Computer

The goal is to install *Immich* (a self-hosted photo/video backup server that supports mobile backup, similar to Google Photos) on a personal computer as the core backup service, and use *Tailscale* (a zero-configuration VPN tool based on WireGuard) to enable remote access (securely exposing the local service to the public network).

This combination is suitable for personal backup scenarios: *Immich* handles backup storage, *Tailscale* solves the intranet penetration problem, requires no complex configuration and is secure and reliable.

## Final Goal

- Immich runs locally at http://localhost:2283
- Expose port 2283 to the public network through Tailscale Funnel
- The mobile App can automatically backup photos/videos at any time using the public domain name

## Stage 1: Install Docker Desktop

### Download Docker Desktop (Official Latest Version)

> https://www.docker.com/products/docker-desktop/

Click "Download for Windows" directly -> Double-click to install (just click Next all the way)

### After installation, the system will automatically restart or prompt to enable WSL2, background update, check "Use WSL2 instead of Hyper-V" → Done.

### Start Docker Desktop (a small whale icon will appear on the desktop, turning green indicates normal operation).

### (Optional but recommended) Set auto-start on boot: Right-click the small whale in the lower right corner → Settings → General → Start Docker Desktop when you log in.

## Stage 2: Deploy Immich with One Click (GUI + Two Commands)

### Create a new folder as the project directory (recommended to place it on a large-capacity disk)

For example: `D:\Immich-Backup` (photos will be stored here, need enough space)

### Right-click in this folder → "Open in Terminal" or "Open PowerShell here"

### Copy and paste the following two commands directly (one line at a time, press Enter to execute):

```powershell
Invoke-WebRequest -Uri https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml -OutFile docker-compose.yml
Invoke-WebRequest -Uri https://github.com/immich-app/immich/releases/latest/download/example.env -OutFile .env
```

### After the download is complete, you will see two more files in the folder: `docker-compose.yml` and `.env`

### Double-click to open the `.env` file (using Notepad or Notepad++), modify the following lines (keep the rest unchanged):

```text
UPLOAD_LOCATION=D:/Immich-Backup/library          # Change to your own absolute path, note the slash is /
DB_DATA_LOCATION=D:/Immich-Backup/postgres        # Same as above
DB_PASSWORD=Set a super strong password like Abc123456!@#   # Must change!
TZ=Asia/Shanghai
```

Save and close.

### Return to the terminal window and start Immich with one click:

```powershell
docker compose up -d
```

The first time will download about 2GB of images, which will take 3~8 minutes with fast internet speed.

### After startup is complete, open http://localhost:2283 in the browser

You will see the Immich registration page → Register the first admin account → Success!

## Stage 3: Use Tailscale for Public Network Access

### Register a Tailscale Account

https://login.tailscale.com

### Install Tailscale Client on Devices to Access Remotely

https://login.tailscale.com/admin

Two devices need to be added here, you can download the app on your phone as another device.

### Enable Funnel

Enter the following command in the terminal to enable Funnel

```bash
tailscale funnel state
```

### Expose Local Service with One Click

```bash
tailscale funnel --https=443 2283
```

### After success, the terminal will immediately display your public network address, for example:

```text
https://beijing-nas.yourname.ts.net
```

Now anyone can directly access this link in the browser to see your local service (actual test in mainland China shows China Telecom/China Unicom/China Mobile basically have 80~150ms latency, very stable in 2025).

### Run in Background, Auto-start on Boot

```bash
tailscale funnel --bg --https=443 2283
```

## Final Testing

### Download Immich App on your phone (official website https://immich.app/ or search for Immich in the app store)

### Open the App → Manually add server → Enter the public network address you just obtained

For example: https://beijing-nas.yourname.ts.net (if you used a custom remote port, include the port; if the panel gives you 80/443, you don't need to write the port)

### Log in with the account you just registered → Enable "Auto Backup" → You will see your phone photos start uploading in a few seconds!

All done! Now your Windows 11 computer has become a personal "Google Photos" that can be accessed anytime, anywhere.
