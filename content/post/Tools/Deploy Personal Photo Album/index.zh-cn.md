---
title: 个人电脑上部署一台随时随地可访问的私人相册
description: Deploy a Personal Photo Album Accessible Anytime, Anywhere on Your Personal Computer
date: '2025-11-24'
categories:
    - Tools
tags:
    - Tools
---

# 个人电脑上部署一台随时随地可访问的私人相册

目标是想在个人电脑上安装*Immich*（一个自托管的照片/视频备份服务器，支持移动端备份，类似于Google Photos）作为核心备份服务，并使用*Tailscale*（一个基于WireGuard的零配置VPN工具）来实现远程访问（将本地服务安全地暴露到公网）。

这个组合适合个人备份场景：*Immich*处理备份存储，*Tailscale*解决内网穿透问题，无需复杂配置且安全可靠。

## 最终目标

- Immich 运行在本地 http://localhost:2283
- 通过 Tailscale Funnel 把 2283 端口穿透到公网
- 手机 App 用公网域名就能随时自动备份照片/视频

## 阶段 1 ： 安装 Docker Desktop

### 下载 Docker Desktop（官方最新版）

> https://www.docker.com/products/docker-desktop/

直接点“Download for Windows” -> 双击安装（一路Next即可）

### 安装完成后会自动重启或提示启用 WSL2，后台更新，勾选“Use WSL2 instead of Hyper-V” → 完成。

### 启动 Docker Desktop（桌面会出现小鲸鱼图标，变绿表示正常）。

### （可选但推荐）设置开机自启：右下角小鲸鱼右键 → Settings → General → Start Docker Desktop when you log in。

## 阶段 2 ： 一键部署Immich（图形化+两行命令）

### 新建一个文件夹当项目目录（建议放在大容量磁盘）

例如：`D:\Immich-Backup` (照片会存这里，空间要够大)

### 在这个文件夹里右键 → “在终端中打开” 或 “PowerShell 这里打开”

### 直接复制粘贴下面两行命令（一次一行，回车执行）：

```powershell
Invoke-WebRequest -Uri https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml -OutFile docker-compose.yml
Invoke-WebRequest -Uri https://github.com/immich-app/immich/releases/latest/download/example.env -OutFile .env
```

### 下载完成后，你会看到文件夹里多了两个文件：`docker-compose.yml` 和 `.env`

### 双击打开 `.env` 文件（用记事本或 Notepad++），修改以下几行（其他保持不动）：

```text
UPLOAD_LOCATION=D:/Immich-Backup/library          # 改成你自己的绝对路径，注意斜杠是 /
DB_DATA_LOCATION=D:/Immich-Backup/postgres        # 同上
DB_PASSWORD=你自己设一个超强密码比如 Abc123456!@#   # 一定要改！
TZ=Asia/Shanghai
```

保存并关闭。

### 回到刚才的终端窗口，一键启动 Immich：

```powershell
docker compose up -d
```

第一次会下载 2GB 左右镜像，网速快的话 3～8 分钟完成。

### 启动完毕后，浏览器打开 http://localhost:2283

看到 Immich 注册页面 → 注册第一个管理员账号 → 成功！

## 阶段 3 ： 用 Tailscale 实现公网访问

### 注册 Tailscale 账号

https://login.tailscale.com

### 在要远程的设备上安装 Tailscale 客户端

https://login.tailscale.com/admin

这里需要两台设备添加进来，可以用手机下载app作为另一个设备。

### 开启 Funnel

终端输入下面的命令，开启Funnel

```bash
tailscale funnel state
```

### 一键暴露本地服务

```bash
tailscale funnel --https=443 2283
```

### 成功后终端会立刻显示你的公网地址，例如：

```text
https://beijing-nas.yourname.ts.net
```

现在任何人都可以直接在浏览器访问这个链接看到你的本地服务了（中国大陆实测电信/联通/移动基本 80~150ms 延迟，2025 年非常稳定）。

### 后台运行，开机自启

```bash
tailscale funnel --bg --https=443 2283
```

## 最终测试

### 手机下载 Immich App（官网 https://immich.app/ 或应用商店搜索 Immich）

### 打开 App → 手动添加服务器 → 输入你刚才拿到的公网地址

例如：https://beijing-nas.yourname.ts.net（如果用了自定义远程端口就要带端口；如果面板给你的是 80/443 可不写端口）

### 用刚才注册的账号登录 → 开启“自动备份” → 几秒后就能看到手机照片开始上传了！

全部完成！现在你的 Windows 11 电脑已经变成一台随时随地可访问的私人“谷歌相册”了。