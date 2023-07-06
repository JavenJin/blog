---
title: Computer Vision - Experiment 7 - Find and draw outline experiments
description: 计算机视觉 - 实验七 查找并绘制轮廓实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验七 查找并绘制轮廓实验

### 实验目的和要求

&emsp;&emsp;理解查找图像轮廓的基本原理；掌握使用OpenCV实现查找轮廓的代码编写方法；掌握使用OpenCV实现绘制轮廓的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用OpenCV中的findContours函数实现查找轮廓；

&emsp;&emsp;（四）使用OpenCV中的drawContours函数实现绘制轮廓。  

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）虽然Canny之类的边缘检测算法可以根据像素之间的差异，检测出轮廓边界的像素，但是它并没有将轮廓作为一个整体。所以，本实验便是把这些边缘像素组装成轮廓。

&emsp;&emsp;（二）一个轮廓一般对应一系列的点，也就是图像中的一条曲线。其表示方法可能根据不同的情况而有所不同。在OpenCV中，可以用findContours函数从二值图像中查找轮廓。drawContours函数用于在图像中绘制外部或内部轮廓 。 

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用findContours函数实现实现查找轮廓；

&emsp;&emsp;（四）编写代码，使用drawContours函数实现实现绘制轮廓。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）findContours函数的功能和使用方法；

&emsp;&emsp;（三）drawContours函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//----------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include <iostream>
using namespace cv;
using namespace std;


//----------------------------【宏定义部分】-------------------------------------------- 
//		描述：定义一些辅助宏 
//------------------------------------------------------------------------------------- 
#define WINDOW_NAME1 "【原始图窗口】"			//为窗口标题定义的宏 
#define WINDOW_NAME2 "【轮廓图】"					//为窗口标题定义的宏 


//----------------------------【全局变量声明部分】--------------------------------------
//		描述：全局变量的声明
//-------------------------------------------------------------------------------------
Mat g_srcImage; 
Mat g_grayImage;
int g_nThresh = 80;
int g_nThresh_max = 255;
RNG g_rng(12345);
Mat g_cannyMat_output;
vector<vector<Point>> g_vContours;
vector<Vec4i> g_vHierarchy;


//----------------------------【全局函数声明部分】--------------------------------------
//		描述：全局函数的声明
//-------------------------------------------------------------------------------------
static void ShowHelpText( );
void on_ThreshChange(int, void* );


//---------------------------【main( )函数】--------------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始执行
//-------------------------------------------------------------------------------------
int main( int argc, char** argv )
{
	//【0】改变console字体颜色
	system("color 1F"); 

	//【0】显示欢迎和帮助文字
	ShowHelpText( );

	// 加载源图像
	g_srcImage = imread( "1.jpg", 1 );
	if(!g_srcImage.data ) { printf("读取图片错误，请确定目录下是否有imread函数指定的图片存在~！ \n"); return false; } 

	// 转成灰度并模糊化降噪
	cvtColor( g_srcImage, g_grayImage, COLOR_BGR2GRAY );
	blur( g_grayImage, g_grayImage, Size(3,3) );

	// 创建窗口
	namedWindow( WINDOW_NAME1, WINDOW_AUTOSIZE );
	imshow( WINDOW_NAME1, g_srcImage );

	//创建滚动条并初始化
	createTrackbar( "canny阈值", WINDOW_NAME1, &g_nThresh, g_nThresh_max, on_ThreshChange );
	on_ThreshChange( 0, 0 );

	waitKey(0);
	return(0);
}

//-----------------------------【on_ThreshChange( )函数】------------------------------  
//      描述：回调函数
//-------------------------------------------------------------------------------------  
void on_ThreshChange(int, void* )
{

	// 用Canny算子检测边缘
	Canny( g_grayImage, g_cannyMat_output, g_nThresh, g_nThresh*2, 3 );
	imshow("canny", g_cannyMat_output);

	// 寻找轮廓
	//void findContours(InputOutputArray image, OutputArrayOfArrays contours,
	//	OutputArray hierarchy, int mode,
	//	int method, Point offset = Point());
	findContours( g_cannyMat_output, g_vContours, g_vHierarchy, RETR_TREE, CHAIN_APPROX_SIMPLE, Point(0, 0) );

	// 绘出轮廓
	Mat drawing = Mat::zeros( g_cannyMat_output.size(), CV_8UC3 );
	for( int i = 0; i< g_vContours.size(); i++ )
	{
		Scalar color = Scalar( g_rng.uniform(0, 255), g_rng.uniform(0,255), g_rng.uniform(0,255) );//任意值
		drawContours( drawing, g_vContours, i, color, 2, 8, g_vHierarchy, 0, Point() );
	}

	// 显示效果图
	imshow( WINDOW_NAME2, drawing );
}


//----------------------------【ShowHelpText( )函数】----------------------------------  
//      描述：输出一些帮助信息  
//-------------------------------------------------------------------------------------  
static void ShowHelpText()  
{  
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第70个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");
	//输出一些帮助信息  
	printf(   "\n\n\t欢迎来到【在图形中寻找轮廓】示例程序~\n\n");  
	printf(   "\n\n\t按键操作说明: \n\n"  
		"\t\t键盘按键任意键- 退出程序\n\n"  
		"\t\t滑动滚动条-改变阈值\n" );  
} 
```

&emsp;&emsp;（二）显示结果

![Find and draw outline experiments 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2007%20Find%20and%20draw%20outline%20experiments/find-and-draw-outline-experiments1.png)

![Find and draw outline experiments 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2007%20Find%20and%20draw%20outline%20experiments/find-and-draw-outline-experiments2.png)

![Find and draw outline experiments 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2007%20Find%20and%20draw%20outline%20experiments/find-and-draw-outline-experiments3.png)

![Find and draw outline experiments 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2007%20Find%20and%20draw%20outline%20experiments/find-and-draw-outline-experiments4.png)

![Find and draw outline experiments 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2007%20Find%20and%20draw%20outline%20experiments/find-and-draw-outline-experiments5.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解查找图像轮廓的基本原理；掌握使用OpenCV实现查找轮廓的代码编写方法；掌握使用OpenCV实现绘制轮廓的代码编写方法。新建工程，在VS2015中配置OpenCV，使用OpenCV中的findContours函数实现查找轮廓；使用OpenCV中的drawContours函数实现绘制轮廓。学会了用findContours函数从二值图像中查找轮廓。drawContours函数用于在图像中绘制外部或内部轮廓。
