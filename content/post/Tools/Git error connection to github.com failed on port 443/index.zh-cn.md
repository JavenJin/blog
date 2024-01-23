---
title: Git报错： Failed to connect to github.com port 443
description: Git error - connection to github.com failed on port 443
date: '2024-01-17'
categories:
    - Tools
tags:
    - Tools
---

# Git报错： Failed to connect to github.com port 443

出现这个问题主要是代理的问题。

一般分为两种情况：

1. 电脑有使用VPN上网，网页可以打开github，说明git在推送/拉取时没有使用vpn进行代理。

2. 电脑没有使用VPN上网，这时可以去某些网站上找一些代理ip+port。

## 解决方案

配置http代理，Windows、Linux、MacOS中git命令相同：

配置socks5代理

```
git config --global http.proxy socks5 127.0.0.1:7890
git config --global https.proxy socks5 127.0.0.1:7890
```

配置http代理

```
git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890
```

注意：

1. **命令中的主机号**（127.0.0.1）是使用代理的主机号（自己电脑有VPN那么本机就是访问github的代理主机，否则是代理主机的ip，也就是网上找的那个ip）。

2. **命令中的端口号**（7890）是代理软件（代理软件如果不显示端口号，需要去代理服务器设置中查看）或代理主机监听的端口。

socks5和http两种协议由所使用的代理软件决定，不同软件对这两种协议的支持有差异，如果不确定可以都尝试一下。

## 查看代理命令

```
git config --global --get http.proxy
git config --global --get https.proxy
```

## 取消代理命令

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```