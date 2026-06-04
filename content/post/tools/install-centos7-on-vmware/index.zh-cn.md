---
title: 在VMware上安装CentOS7
description: Install CentOS7 on VMware
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

![](images/image01.png)

## 安装CentOS 7

### 打开VMware软件，点击创建新的虚拟机，打开新建虚拟机向导

![](images/image02.png)

### 选择自定义（高级），点击下一步

![](images/image03.png)

### 选择Workstation 15.x，点击下一步

![](images/image04.png)

### 选择稍后安装操作系统，点击下一步

![](images/image05.png)

### 客户机操作系统选择Linux，版本选择CentOS 7 64位，点击下一步

![](images/image06.png)

### 修改虚拟机名称，和虚拟机存储路径后点击下一步

![](images/image07.png)

### 虚拟机处理器数量和内核数量都选择2，点击下一步

![](images/image08.png)

### 选择虚拟机内存为1GB，点击下一步

![](images/image09.png)

### 选择使用网络地址转换（NAT）后点击下一步

![](images/image10.png)

### 选择LSI Logic，点击下一步

![](images/image11.png)

### 硬盘类型选择SCSI，点击下一步

![](images/image12.png)

### 选择创建新虚拟硬盘，点击下一步

![](images/image13.png)

### 最大磁盘大侠设置为20G，选择将虚拟磁盘拆分成多个文件，点击下一步

![](images/image14.png)

### 设置磁盘文件名后点击下一步

![](images/image15.png)

### 点击完成

![](images/image16.png)

### 点击编辑虚拟机设置

![](images/image17.png)

### 左侧选择CD/DVD，选择使用ISO映像文件，点击浏览，选择CentOS-7-x86_64-DVD-1611.iso镜像文件，点击确定

![](images/image18.png)

### 点击开启此虚拟机，等待虚拟机启动

![](images/image19.png)

### 使用键盘上下选择Install CentOS Linux 7回车

![](images/image20.png)

### 等待系统自检

![](images/image21.png)

### 选择中文，点击继续

![](images/image22.png)

### 点击软件选择

![](images/image23.png)

### 勾选需要的功能（这里我只需要最小安装即可），点击完成

![](images/image24.png)

### 点击安装位置

![](images/image25.png)

### 点击完成

![](images/image26.png)

### 点击开始安装

![](images/image27.png)

### 点击ROOT密码

![](images/image28.png)

### 设置密码后，点击完成

![](images/image29.png)

### 由于密码过于简单，需二次确认密码，再次点击完成

![](images/image30.png)

### 等待系统安装完毕后点击重启即可使用

![](images/image31.png)