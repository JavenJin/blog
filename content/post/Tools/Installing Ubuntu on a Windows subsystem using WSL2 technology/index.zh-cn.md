---
title: Install Ubuntu on Windows subsystem using WSL2 technology
description: 使用WSL2技术在Windows子系统上安装Ubuntu
date: '2022-09-16'
categories:
    - Tools
tags:
    - Tools
---

# 使用WSL2技术在Windows子系统上安装Ubuntu

## 安装WSL2

参考资料：[Manual installation steps for older versions of WSL](https://docs.microsoft.com/en-us/windows/wsl/install-manual)

### 为 Linux 启用 Windows 子系统

以管理员身份打开 PowerShell （开始菜单 > PowerShell > 右键单击 > 以管理员身份运行）并输入以下命令：

```sh
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

### 启动虚拟机功能

以管理员身份打开 PowerShell 并运行：

```sh
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### 重启计算机

### 下载 Linux 内核更新包并安装

下载地址1（Microsoft官网下载）：[Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

下载地址2（csdn下载）：[Linux 内核更新包](https://download.csdn.net/download/weixin_42718701/86540810)

运行下载的更新包。（双击运行 - 系统将提示您提升权限，选择“是”以批准此安装。）

### 将 WSL2 设置为默认版本

打开 PowerShell 并运行以下命令，将 WSL 2 设置为安装新 Linux 发行版时的默认版本：

```sh
wsl --set-default-version 2
```

## 安装Ubuntu并安装docker及docker-compose

安装Ubuntu参考资料：[https://docs.microsoft.com/en-us/windows/wsl/install-manual](https://docs.microsoft.com/en-us/windows/wsl/install-manual)

安装docker参考资料：[https://www.runoob.com/docker/ubuntu-docker-install.html](https://www.runoob.com/docker/ubuntu-docker-install.html)

安装docker-compose参考资料：[https://linuxhostsupport.com/blog/how-to-install-and-configure-docker-compose-on-ubuntu-20-04/](https://linuxhostsupport.com/blog/how-to-install-and-configure-docker-compose-on-ubuntu-20-04/)

### 打开[Microsoft Store](https://aka.ms/wslstore)并选择Ubuntu版本进行下载

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-1.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-2.png)

### 等待自动安装成功

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-3.png)

### 启动Ubuntu，等待自动安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-4.png)

### 设置用户名及密码后进入Ubuntu系统中

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-5.png)

### Ubuntu Docker安装

使用国内 daocloud 一键安装命令：

安装命令如下：

```sh
sudo curl -sSL https://get.daocloud.io/docker | sh
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-6.png)

等待安装成功

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-7.png)

启动docker服务命令

```sh
sudo service docker start
```

查看是否安装成功命令

```
sudo docker ps -a
```

显示如下即安装Ubuntu Docker成功

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-8.png)

### 安装docker-compose

更新apt-get命令：

```sh
sudo apt-get update -y
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-9.png)

安装docker-compose命令：

```sh
sudo apt-get install docker-compose
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-10.png)

中途输入y回车即可

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Installing%20Ubuntu%20on%20a%20Windows%20subsystem%20using%20WSL2%20technology/install-ubuntu-on-windows-subsystem-using-wsl2-technology-11.png)

安装完成！