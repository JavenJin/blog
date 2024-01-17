---
title: Git error - connection to github.com failed on port 443
description: Git报错： Failed to connect to github.com port 443
date: '2024-01-17'
categories:
    - Tools
tags:
    - Tools
---

# Git error: connection to github.com failed on port 443

This problem occurs mainly with proxies.

There are two general categories:

1. The computer has internet access using a VPN, and the webpage can open github, indicating that git is not proxied using a vpn when pushing/pulling.

2. The computer is not using a VPN to access the internet, at this point you can go to certain websites and find some proxy ip+port.

## Solution

Configure the http proxy, the git command is the same in Windows, Linux and MacOS:

Configuring the socks5 proxy

```
git config --global http.proxy socks5 127.0.0.1:7890
git config --global https.proxy socks5 127.0.0.1:7890
```

Configuring the http proxy

```
git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890
```

Note:

1. The **host number** (127.0.0.1) in the command is the host number of the proxy being used (your own computer has a VPN then the local machine is the proxy host for accessing github, otherwise it's the ip of the proxy host, which is the same ip you find online).

2. The **port number** (7890) in the command is the port on which the proxy software (if the proxy software does not show the port number, you need to go to the proxy server settings to check it) or the proxy host is listening.

The two protocols, socks5 and http, are determined by the proxy software used, and support for these two protocols varies from software to software, so if you're not sure you can try them both.

## View Proxy Command

```
git config --global --get http.proxy
git config --global --get https.proxy
```

## Cancel Proxy Command

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```