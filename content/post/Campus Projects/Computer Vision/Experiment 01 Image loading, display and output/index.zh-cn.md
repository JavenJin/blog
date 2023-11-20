---
title: 计算机视觉 - 实验一 图像的载入、显示与输出
description: Computer Vision - Experiment 1 - Image loading, display and output
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验一 图像的载入、显示与输出

### 实验目的和要求

&emsp;&emsp;（一）通过实验掌握 Windows 中安装 OpenCV 的方法；

&emsp;&emsp;（二）通过实验掌握图像的载入、显示与输出的方法

### 实验内容

&emsp;&emsp;（一）Windows中安装OpenCV;

&emsp;&emsp;（二）编写图像的载入、显示与输出的程序.

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows 7 操作系统和 Visual Studio 2015

### 实验原理

&emsp;&emsp;Opencv用 Mat类来实现图像的存储。图像存储在矩阵格式中，每个像素都有个位置，可以通过列数和行数引用。Mat类不只用于存储图像，而且还可以存储任意大小的不同类型的矩阵。可以使用Mat类执行矩阵加法、矩阵乘法、创建矩阵等操作。imread函数用于读取图像。imwrite函数用于写图像。imshow函数用于显示图像。

### 实验步骤

&emsp;&emsp;（一）Windows中安装OpenCV

&emsp;&emsp;在网址[https://sourceforge.net/projects/opencvlibrary/](https://sourceforge.net/projects/opencvlibrary/)中下载opencv源代码，在Windows中安装OpenCV。

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用imread函数读取图像；

&emsp;&emsp;（四）编写代码，使用imwrite函数写图像；

&emsp;&emsp;（五）编写代码，使用imshow函数显示图像。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）imread、imwrite、imshow函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
using namespace cv;


int main( )
{
	//-------------------------------【一、图像的载入和显示】----------------------------
	//	描述：以下三行代码用于完成图像的载入和显示
	//---------------------------------------------------------------------------------
	
	cv::Mat girl = cv::imread("girl.jpg", 0); //载入图像到Mat
	namedWindow("【1】动漫图"); //创建一个名为 "【1】e动漫图"的窗口  
	imshow("【1】动漫图",girl);//显示名为 "【1】动漫图"的窗口  

	//-------------------------------【二、初级图像混合】---------------------------------
	//	描述：二、初级图像混合
	//---------------------------------------------------------------------------------
	//载入图片
	Mat image = imread("dota.jpg");
	Mat logo = imread("dota_logo.jpg");

	//载入后先显示
	namedWindow("【2】原画图");
	imshow("【2】原画图",image);

	namedWindow("【3】logo图");
	imshow("【3】logo图",logo);

	// 定义一个Mat类型，用于存放，图像的ROI
	Mat imageROI;
	//方法一
	imageROI= image(Rect(800,350,logo.cols,logo.rows));
	//方法二
	//imageROI= image(Range(350,350+logo.rows),Range(800,800+logo.cols));

	// 将logo加到原图上
	addWeighted(imageROI,0.5,logo,0.3,0.,imageROI);

	//显示结果
	namedWindow("【4】原画+logo图");
	imshow("【4】原画+logo图",image);

	//--------------------------------【三、图像的输出】----------------------------------
	//	描述：将一个Mat图像输出到图像文件
	//---------------------------------------------------------------------------------
	//输出一张jpg图片到工程目录下
	imwrite("由imwrite生成的图片.jpg", image);
	//imwrite("由imwrite生成的图片.jpg", image);

	waitKey(0);

	return 0;
}
```

&emsp;&emsp;（二）显示结果


![Image loading, display and output 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output1.jpeg)

![Image loading, display and output 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output2.jpeg)

![Image loading, display and output 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output3.jpeg)

![Image loading, display and output 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output4.jpeg)

![Image loading, display and output 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output5.jpeg)

![Image loading, display and output 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output6.jpeg)

### 实验总结

&emsp;&emsp;本次实验的主要内容是编写图像的载入、显示与输出的程序。用到的函数主要有cv::Mat girl=cv::imread("xx.jpg", 0);（载入图像到Mat，第一个参数xx.jpg是图片名称，第二个参数0是灰度图）；namedWindow("窗口名称"); ；显示函数imshow("窗口名称",xx); ；载入图片函数Mat image= imread("xx.jpg"); ；imageROI= image(Rect());；addWeighted();；imwrite(".jpg",image); ；等等函数。本次试验让我充分理解了上述的函数以及试验流程。学会了自己使用上述函数进行图片最基本的载入、显示与输入。
