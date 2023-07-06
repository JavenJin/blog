---
title: Install CentOS7 on VMware
description: 在VMware上安装CentOS7
date: '2021-08-16'
categories:
    - Tools
tags:
    - Tools
---

# 在VMware上安装CentOS7

## 安装前准备

- 电脑上安装VMware Workstation 15.5 Pro

- 下载CentOS-7-x86_64-DVD-1611.iso镜像文件

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-1.png)

## 安装CentOS 7

### 打开VMware软件，点击创建新的虚拟机，打开新建虚拟机向导

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-2.png)

### 选择自定义（高级），点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-3.png)

### 选择Workstation 15.x，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-4.png)

### 选择稍后安装操作系统，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-5.png)

### 客户机操作系统选择Linux，版本选择CentOS 7 64位，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-6.png)

### 修改虚拟机名称，和虚拟机存储路径后点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-7.png)

### 虚拟机处理器数量和内核数量都选择2，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-8.png)

### 选择虚拟机内存为1GB，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-9.png)

### 选择使用网络地址转换（NAT）后点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-10.png)

### 选择LSI Logic，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-11.png)

### 硬盘类型选择SCSI，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-12.png)

### 选择创建新虚拟硬盘，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-13.png)

### 最大磁盘大侠设置为20G，选择将虚拟磁盘拆分成多个文件，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-14.png)

### 设置磁盘文件名后点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-15.png)

### 点击完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-16.png)

### 点击编辑虚拟机设置

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-17.png)

### 左侧选择CD/DVD，选择使用ISO映像文件，点击浏览，选择CentOS-7-x86_64-DVD-1611.iso镜像文件，点击确定

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-18.png)

### 点击开启此虚拟机，等待虚拟机启动

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-19.png)

### 使用键盘上下选择Install CentOS Linux 7回车

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-20.png)

### 等待系统自检

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-21.png)

### 选择中文，点击继续

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-22.png)

### 点击软件选择

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-23.png)

### 勾选需要的功能（这里我只需要最小安装即可），点击完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-24.png)

### 点击安装位置

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-25.png)

### 点击完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-26.png)

### 点击开始安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-27.png)

### 点击ROOT密码

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-28.png)

### 设置密码后，点击完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-29.png)

### 由于密码过于简单，需二次确认密码，再次点击完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-30.png)

### 等待系统安装完毕后点击重启即可使用

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20CentOS7%20on%20VMware/install-centos7-on-vmware-31.png)