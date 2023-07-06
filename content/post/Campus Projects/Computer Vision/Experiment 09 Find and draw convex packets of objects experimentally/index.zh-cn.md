---
title: Computer Vision - Experiment 9 - Find and draw convex packets of objects experimentally
description: 计算机视觉 - 实验九 寻找和绘制物体的凸包实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验九 寻找和绘制物体的凸包实验

### 实验目的和要求

&emsp;&emsp;理解使用凸包的基本原理；掌握使用OpenCV通过凸包理解物体形状或轮廊的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用OpenCV中的findContours函数查找图像轮廓；

&emsp;&emsp;（四）遍历每个轮廓，使用OpenCV中的convexHull寻找其凸包；

&emsp;&emsp;（五）编写代码，使用OpenCV中的drawContours函数绘出图像轮廓及其凸包。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）凸包(Convex Hull)是一个计算几何(图形学)中常见的概念。简单来说，给定二维平面上的点集，凸包就是将最外层的点连接起来构成的凸多边型，它是能包含点集中所有点的。理解物体形状或轮廊的一种比较有用的方法便是计算一个物体的凸包。

&emsp;&emsp;（二）在OpenCV中，convexHull函数用于寻找图像点集的凸包。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用findContours函数查找图像轮廓；

&emsp;&emsp;（四）编写代码，遍历每个轮廓，使用convexHull函数寻找其凸包；

&emsp;&emsp;（五）编写代码，绘出图像轮廓及其凸包。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）findContours函数的功能和使用方法；

&emsp;&emsp;（三）convexHull函数的功能和使用方法；

&emsp;&emsp;（四）drawContours函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//---------------------------------【头文件、命名空间包含部分】---------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include <iostream>
using namespace cv;
using namespace std;


//-----------------------------------【宏定义部分】----------------------------------
//  描述：定义一些辅助宏 
//-------------------------------------------------------------------------------------
#define WINDOW_NAME1 "【原始图窗口】"					//为窗口标题定义的宏 
#define WINDOW_NAME2 "【效果图窗口】"					//为窗口标题定义的宏 



//-----------------------------------【全局变量声明部分】-------------------------------
//  描述：全局变量的声明
//------------------------------------------------------------------------------------
Mat g_srcImage; Mat g_grayImage;
int g_nThresh = 50;
int g_maxThresh = 255;
RNG g_rng(12345);
Mat srcImage_copy = g_srcImage.clone();
Mat g_thresholdImage_output;
vector<vector<Point> > g_vContours;
vector<Vec4i> g_vHierarchy;


//----------------------------【全局函数声明部分】--------------------------------------
//   描述：全局函数的声明
//-------------------------------------------------------------------------------------
static void ShowHelpText( );
void on_ThreshChange(int, void* );
void ShowHelpText();

//-----------------------【main( )函数】------------------------------------------
//   描述：控制台应用程序的入口函数，我们的程序从这里开始执行
//------------------------------------------------------------------------------------
int main(  )
{
	system("color 3F");
	ShowHelpText();

	// 加载源图像
	g_srcImage = imread( "2007_000804.jpg", 1 );

	// 将原图转换成灰度图并进行模糊降
	cvtColor( g_srcImage, g_grayImage, COLOR_BGR2GRAY );
	blur( g_grayImage, g_grayImage, Size(3,3) );

	// 创建原图窗口并显示
	namedWindow( WINDOW_NAME1, WINDOW_AUTOSIZE );
	imshow( WINDOW_NAME1, g_srcImage );

	//创建滚动条
	createTrackbar( " 阈值:", WINDOW_NAME1, &g_nThresh, g_maxThresh, on_ThreshChange );
	on_ThreshChange( 0, 0 );//调用一次进行初始化

	waitKey(0);
	return(0);
}

//---------------------------【thresh_callback( )函数】----------------------------------
//      描述：回调函数
//-------------------------------------------------------------------------------------
void on_ThreshChange(int, void* )
{
	// 对图像进行二值化，控制阈值
	threshold( g_grayImage, g_thresholdImage_output, g_nThresh, 255, THRESH_BINARY );

	// 寻找轮廓
	findContours( g_thresholdImage_output, g_vContours, g_vHierarchy, RETR_TREE, CHAIN_APPROX_SIMPLE, Point(0, 0) );

	// 遍历每个轮廓，寻找其凸包
	vector<vector<Point> >hull( g_vContours.size() );
	for( unsigned int i = 0; i < g_vContours.size(); i++ )
	{  
		convexHull( Mat(g_vContours[i]), hull[i], false );
	}

	// 绘出轮廓及其凸包
	Mat drawing = Mat::zeros( g_thresholdImage_output.size(), CV_8UC3 );
	Mat drawing1;
	cv::cvtColor(g_grayImage, drawing1, cv::COLOR_GRAY2BGR);
	Mat drawing2 = Mat::zeros(g_thresholdImage_output.size(), CV_8UC3);

	for(unsigned  int i = 0; i< g_vContours.size(); i++ )
	{
		Scalar color = Scalar( g_rng.uniform(0, 255), g_rng.uniform(0,255), g_rng.uniform(0,255) );
		drawContours( drawing, g_vContours, i, color, 1, 8, vector<Vec4i>(), 0, Point() );
		drawContours( drawing, hull, i, color, 1, 8, vector<Vec4i>(), 0, Point() );
		drawContours( drawing1, hull, i, color, 1, 8, vector<Vec4i>(), 0, Point() );
		drawContours(drawing2, g_vContours, i, color, 1, 8, vector<Vec4i>(), 0, Point() );
	}

	// 显示效果图
	imshow( WINDOW_NAME2, drawing );
	imshow( "hull", drawing1);
	imshow( "Contours", drawing2);
}


//-----------------------------------【ShowHelpText( )函数】-----------------------------
//		 描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
void ShowHelpText()
{
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第72个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n------------------------------------------------------------------\n");
}
```

&emsp;&emsp;（二）显示结果

![Find and draw convex packets of objects experimentally 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2009%20Find%20and%20draw%20convex%20packets%20of%20objects%20experimentally/find-and-draw-convex-packets-of-objects-experimentally1.png)

![Find and draw convex packets of objects experimentally 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2009%20Find%20and%20draw%20convex%20packets%20of%20objects%20experimentally/find-and-draw-convex-packets-of-objects-experimentally2.png)

![Find and draw convex packets of objects experimentally 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2009%20Find%20and%20draw%20convex%20packets%20of%20objects%20experimentally/find-and-draw-convex-packets-of-objects-experimentally3.png)

![Find and draw convex packets of objects experimentally 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2009%20Find%20and%20draw%20convex%20packets%20of%20objects%20experimentally/find-and-draw-convex-packets-of-objects-experimentally4.png)

![Find and draw convex packets of objects experimentally 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2009%20Find%20and%20draw%20convex%20packets%20of%20objects%20experimentally/find-and-draw-convex-packets-of-objects-experimentally5.png)

![Find and draw convex packets of objects experimentally 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2009%20Find%20and%20draw%20convex%20packets%20of%20objects%20experimentally/find-and-draw-convex-packets-of-objects-experimentally6.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解使用凸包的基本原理；掌握使用OpenCV通过凸包理解物体形状或轮廊的代码编写方法。新建工程，在VS2015中配置OpenCV，使用OpenCV中的findContours函数查找图像轮廓；遍历每个轮廓，使用OpenCV中的convexHull寻找其凸包；编写代码，使用OpenCV中的drawContours函数绘出图像轮廓及其凸。学会了用findContours函数查找图像轮廓；学会了使用convexHull函数寻找其凸包；学会了使用drawContours函数绘出图像轮廓及其凸。