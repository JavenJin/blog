---
title: 在Windows上安装Tomcat8
description: Install Tomcat8 on Windows
date: '2021-07-26'
slug: install-tomcat8-on-windows
categories:
    - Tools
tags:
    - Tools
---

# 在Windows上安装Tomcat8

## 下载安装包

**访问Tomcat官网 [https://tomcat.apache.org/](https://tomcat.apache.org/)**

![](images/image01.png)

**在左侧Download栏选择下载版本，这里选择的是Tomcat8版本，点击进入**

![](images/image02.png)

**根据自己系统版本选择对应版本下载，这里选择的是Windows64位操作系统版本，如图点击下载**

![](images/image03.png)

## 安装Tomcat8（下载的zip包为免安装版，解压后可直接使用）

**将下载下来的文件解压**

![](images/image04.png)

**将解压的文件放在D盘**

![](images/image05.png)

## 配置环境变量

**在此电脑上右键点击属性，打开设置**

![](images/image06.png)

**点击高级系统设置，打开系统属性**

![](images/image07.png)

**点击环境变量，打开环境变量**

![](images/image08.png)

**选中path，点击编辑，进入编辑path变量页面**

![](images/image09.png)

**点击新建，输入Tomcat8的安装目录下bin文件夹的目录，点击确定，确定，确定**

![](images/image10.png)

## 运行命令

**进入Tomcat8安装目录下bin文件夹中**

![](images/image11.png)

**点击地址栏，输入cmd，回车，打开命令行窗口**

![](images/image12.png)

**在命令行窗口中输入service.bat install后回车**

![](images/image13.png)

**显示如图即为安装成功**

## 测试是否成功

**双击运行bin文件夹下的Tomcat8w.exe文件，打开启动窗口**

![](images/image14.png)

**点击Start启动Tomcat8**

![](images/image15.png)

**打开浏览器，输入127.0.0.1:8080访问出现如下画面即为安装成功**

![](images/image16.png)
