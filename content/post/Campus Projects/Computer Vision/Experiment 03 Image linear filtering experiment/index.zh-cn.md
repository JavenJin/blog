---
title: 计算机视觉 - 实验三 图像线性滤波实验
description: Computer Vision - Experiment 3 - Image linear filtering experiment
date: '2020-03-16'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验三 图像线性滤波实验

### 实验目的和要求

&emsp;&emsp;（一）通过实验掌握图像的方框滤波原理和编程实现方法； 

&emsp;&emsp;（二）通过实验掌握图像的均值滤波原理和编程实现方法；

&emsp;&emsp;（二）通过实验掌握图像的高斯滤波原理和编程实现方法。

### 实验内容

&emsp;&emsp;（一）使用OpenCV中的boxFilter函数实现方框滤波;

&emsp;&emsp;（二）使用OpenCV中的blur函数实现均值滤波；

&emsp;&emsp;（三）使用OpenCV中的GaussianBlur函数实现高斯滤波。  

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015 

### 实验原理

&emsp;&emsp;（一）图像滤波，指在尽量保留图像细节特征的条件下对目标图像的噪声进行抑制，是图像预处理中不可缺少的操作，其处理效果的好坏将直接影响到后续图像处理和分析的有效性和可靠性。线性滤波器每个像素的输出值是一些输入像素的加权和。线性滤波器易于构造，井且易于从频率响应角度来进行分析。 

&emsp;&emsp;（二）在OpenCV中，提供了如下三种常用的线性滤波操作，它们分别被封装在单独的函数中，使用起来非常方便，分别是：方框滤波boxFilter函数，均值滤波blur函数；高斯滤波GaussianBlur函数。 

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用boxFilter函数实现方框滤波；

&emsp;&emsp;（四）编写代码，使用blur函数实现均值滤波；

&emsp;&emsp;（五）编写代码，使用gaussianBlur函数实现高斯滤波。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）boxFilter函数、blur函数、gaussianBlur函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//------------------------------【头文件、命名空间包含部分】------------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>
#include <iostream>

using namespace std;
using namespace cv;


//----------------------------------【全局变量声明部分】---------------------------------
//	描述：全局变量声明
//-------------------------------------------------------------------------------------
Mat g_srcImage,g_dstImage1,g_dstImage2,g_dstImage3;//存储图片的Mat类型
int g_nBoxFilterValue=3;  //方框滤波参数值
int g_nMeanBlurValue=3;  //均值滤波参数值
int g_nGaussianBlurValue=3;  //高斯滤波参数值


//---------------------------------【全局函数声明部分】----------------------------------
//	描述：全局函数声明
//-------------------------------------------------------------------------------------
//四个轨迹条的回调函数
static void on_BoxFilter(int, void *);		//方框滤波
static void on_MeanBlur(int, void *);		//均值滤波
static void on_GaussianBlur(int, void *);			//高斯滤波
void ShowHelpText();


//----------------------------------【main( )函数】------------------------------------
//	描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main(   )
{
	//改变console字体颜色
	system("color 5F");  

	//输出帮助文字
	ShowHelpText();

	// 载入原图
	g_srcImage = imread( "20170829110313260.png", 1 );
	if( !g_srcImage.data ) { printf("Oh，no，读取srcImage错误~！ \n"); return false; }

	//克隆原图到三个Mat类型中
	g_dstImage1 = g_srcImage.clone( );
	g_dstImage2 = g_srcImage.clone( );
	g_dstImage3 = g_srcImage.clone( );

	//显示原图
	namedWindow("【<0>原图窗口】", 1);
	imshow("【<0>原图窗口】",g_srcImage);


	//=================【<1>方框滤波】==================
	//创建窗口
	namedWindow("【<1>方框滤波】", 1);
	//创建轨迹条
	createTrackbar("内核值：", "【<1>方框滤波】", &g_nBoxFilterValue, 40, on_BoxFilter);
	on_BoxFilter(g_nBoxFilterValue, 0);
	//================================================

	//=================【<2>均值滤波】==================
	//创建窗口
	namedWindow("【<2>均值滤波】", 1);
	//创建轨迹条
	createTrackbar("内核值：", "【<2>均值滤波】",&g_nMeanBlurValue, 40,on_MeanBlur );
	on_MeanBlur(g_nMeanBlurValue,0);
	//================================================

	//=================【<3>高斯滤波】=====================
	//创建窗口
	namedWindow("【<3>高斯滤波】", 1);
	//创建轨迹条
	createTrackbar("内核值：", "【<3>高斯滤波】",&g_nGaussianBlurValue, 40,on_GaussianBlur );
	on_GaussianBlur(g_nGaussianBlurValue,0);
	//================================================


	//输出一些帮助信息
	cout<<endl<<"\t运行成功，请调整滚动条观察图像效果~\n\n"
		<<"\t按下“q”键时，程序退出。\n";

	//按下“q”键时，程序退出
	while(char(waitKey(1)) != 'q') {}

	return 0;
}


//----------------------------【on_BoxFilter( )函数】------------------------------------
//	描述：方框滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_BoxFilter(int, void *)
{
	//方框滤波操作，其主要功能是：在给定的滑动窗口大小下，对每个窗口内的像素值进行快速相加求和
	boxFilter( g_srcImage, g_dstImage1, -1,Size( g_nBoxFilterValue+1, g_nBoxFilterValue+1));
	//显示窗口
	imshow("【<1>方框滤波】", g_dstImage1);
}


//-----------------------------【on_MeanBlur( )函数】------------------------------------
//	描述：均值滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_MeanBlur(int, void *)
{
	//均值滤波操作，均值滤波是一种典型的线性滤波算法，主要是利用像素点邻域的像素值来计算像素点的值。
	//其具体方法是首先给出一个滤波模板kernel，该模板将覆盖像素点周围的其他邻域像素点，
	//去掉像素本身，将其邻域像素点相加然后取平均值即为该像素点的新的像素值，这就是均值滤波的本质。
	//. Size ksize : 滤波模板kernel的尺寸，一般使用Size(w, h)来指定，如Size(3, 3)
	//.Point anchor = Point(-1, -1) : 字面意思是锚点，也就是处理的像素位于kernel的什么位置，
	//默认值为(-1, -1)即位于kernel中心点，如果没有特殊需要则不需要更改
	blur( g_srcImage, g_dstImage2, Size( g_nMeanBlurValue+1, g_nMeanBlurValue+1), Point(-1,-1));
	//显示窗口
	imshow("【<2>均值滤波】", g_dstImage2);
}


//-----------------------------【ContrastAndBright( )函数】------------------------------
//	描述：高斯滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_GaussianBlur(int, void *)
{
	//高斯滤波操作
	//void GaussianBlur(InputArray src, OutputArray dst, Size ksize,
	//	double sigmaX, double sigmaY = 0,
	//	int borderType = BORDER_DEFAULT);
	//. double sigmaX : 高斯核函数在X方向上的标准偏差
	//. double sigmaY : 高斯核函数在Y方向上的标准偏差
	//如果sigmaX和sigmaY都是0，这两个值将由ksize.width和ksize.height计算而来。
	//具体可以参考getGaussianKernel()函数查看具体细节。
	GaussianBlur( g_srcImage, g_dstImage3, Size( g_nGaussianBlurValue*2+1, g_nGaussianBlurValue*2+1 ), 0, 0);
	//显示窗口
	imshow("【<3>高斯滤波】", g_dstImage3);
}


//--------------------------------【ShowHelpText( )函数】--------------------------------
//		 描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
void ShowHelpText()
{
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第34个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");
}
```

&emsp;&emsp;（二）显示结果

![Image linear filtering experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment1.png)

![Image linear filtering experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment2.png)

![Image linear filtering experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment3.png)

![Image linear filtering experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment4.png)

![Image linear filtering experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment5.png)

![Image linear filtering experiment 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment6.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是掌握图像的方框滤波原理和编程实现方法、掌握图像的均值滤波原理和编程实现方法、掌握图像的高斯滤波原理和编程实现方法。使用OpenCV中的boxFilter函数实现方框滤波、使用OpenCV中的blur函数实现均值滤波、使用OpenCV中的GaussianBlur函数实现高斯滤波。通过编写代码，我学会了使用boxFilter函数、blur函数和GaussianBlur函数实现方框滤波、均值滤波和高斯滤波。
