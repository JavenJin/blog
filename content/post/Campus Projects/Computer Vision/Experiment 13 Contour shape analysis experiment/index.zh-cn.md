---
title: Computer Vision - Experiment 13 - Contour shape analysis experiment
description: 计算机视觉 - 实验十三 轮廓形状分析实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验十三 轮廓形状分析实验

### 实验目的和要求

&emsp;&emsp;理解轮廓形状分析的基本原理；掌握实现轮廓形状分析的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）得到原图的灰度图像并进行平滑；

&emsp;&emsp;（四）使用Threshold检测边缘；

&emsp;&emsp;（五）找出轮廓;

&emsp;&emsp;（六）多边形逼近轮廓，获取矩形和圆形边界框；

&emsp;&emsp;（七）绘制多边形轮廓、包围的矩形框和圆形框。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015。

### 实验原理

&emsp;&emsp;（一）在计算机视觉中，形状特征是描述高层视觉特征(如目标，对象)的重要手段。目标、对象对获取图像语义尤为重要，所以必须有好的形状特征的提取和描述算法。轮廓形状分析是提取形状特征的一种重要途径。

&emsp;&emsp;（二）本实验首先找出目标轮廓，然后用指定精度逼近多边形曲线，接着计算点集的最外面矩形边界，寻找最小面积的包围圆形，最后绘制多边形轮廓、包围的矩形框、圆形框，比较提取的三种轮廓形状对目标对象的描述效果。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）得到原图的灰度图像并进行平滑；

&emsp;&emsp;（四）使用OpenCV中的threshold函数二值化；

&emsp;&emsp;（五）使用OpenCV中的findContours函数找出轮廓;

&emsp;&emsp;（六）使用OpenCV中的approxPolyDP函数多边形逼近轮廓，使用OpenCV中的boundingRect函数获取矩形，使用OpenCV中的minEnclosingCircle函数圆形边界框；

&emsp;&emsp;（七）使用OpenCV中的drawContours函数绘制多边形轮廓、使用OpenCV中的rectangle函数绘制包围的矩形框，使用OpenCV中的circle函数绘制包围的圆形框。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）threshold函数的功能和使用方法；

&emsp;&emsp;（三）approxPolyDP函数的功能和使用方法；

&emsp;&emsp;（四）rectangle函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//---------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//------------------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
using namespace cv;
using namespace std;

//-----------------------------------【宏定义部分】-------------------------------------------- 
//  描述：定义一些辅助宏 
//------------------------------------------------------------------------------------------------ 
#define WINDOW_NAME1 "【原始图窗口】"        //为窗口标题定义的宏 
#define WINDOW_NAME2 "【效果图窗口】"        //为窗口标题定义的宏 

//-----------------------------------【全局变量声明部分】--------------------------------------
//  描述：全局变量的声明
//-----------------------------------------------------------------------------------------------
Mat g_srcImage;
Mat g_grayImage;
int g_nThresh = 50;//阈值
int g_nMaxThresh = 255;//阈值最大值
RNG g_rng(12345);//随机数生成器

//-----------------------------------【全局函数声明部分】--------------------------------------
//   描述：全局函数的声明
//-----------------------------------------------------------------------------------------------
void on_ContoursChange(int, void* );
static void ShowHelpText( );

//-----------------------------------【main( )函数】--------------------------------------------
//   描述：控制台应用程序的入口函数，我们的程序从这里开始执行
//-----------------------------------------------------------------------------------------------
int main( )
{
	//【0】改变console字体颜色
	system("color 1F"); 

	//【0】显示欢迎和帮助文字
	ShowHelpText( );

	//【1】载入3通道的原图像
	g_srcImage = imread( "2007_000837.jpg", 1 );
	if(!g_srcImage.data ) { printf("读取图片错误，请确定目录下是否有imread函数指定的图片存在~！ \n"); return false; }  

	//【2】得到原图的灰度图像并进行平滑
	cvtColor( g_srcImage, g_grayImage, COLOR_BGR2GRAY );
	blur( g_grayImage, g_grayImage, Size(3,3) );

	//【3】创建原始图窗口并显示
	namedWindow( WINDOW_NAME1, WINDOW_AUTOSIZE );
	imshow( WINDOW_NAME1, g_srcImage );

	//【4】设置滚动条并调用一次回调函数
	createTrackbar( " 阈值:", WINDOW_NAME1, &g_nThresh, g_nMaxThresh, on_ContoursChange );
	on_ContoursChange( 0, 0 );

	waitKey(0);

	return(0);
}

//----------------------------【on_ContoursChange( )函数】---------------------------------
//      描述：回调函数
//-------------------------------------------------------------------------------------------------  
void on_ContoursChange(int, void* )
{
	//定义一些参数
	Mat threshold_output;
	vector<vector<Point>> contours;
	vector<Vec4i> hierarchy;

	// 使用Threshold检测边缘
	threshold( g_grayImage, threshold_output, g_nThresh, 255, THRESH_BINARY );

	// 找出轮廓
	findContours( threshold_output, contours, hierarchy, RETR_TREE, CHAIN_APPROX_SIMPLE, Point(0, 0) );

	// 多边形逼近轮廓 + 获取矩形和圆形边界框
	vector<vector<Point> > contours_poly( contours.size() );
	vector<Rect> boundRect( contours.size() );
	vector<Point2f>center( contours.size() );
	vector<float>radius( contours.size() );

	//一个循环，遍历所有部分，进行本程序最核心的操作
	for( unsigned int i = 0; i < contours.size(); i++ )
	{ 
		approxPolyDP( Mat(contours[i]), contours_poly[i], 3, true );//用指定精度逼近多边形曲线 
		boundRect[i] = boundingRect( Mat(contours_poly[i]) );//计算点集的最外面（up-right）矩形边界
		minEnclosingCircle( contours_poly[i], center[i], radius[i] );//对给定的 2D点集，寻找最小面积的包围圆形 
	}

	// 绘制多边形轮廓 + 包围的矩形框 + 圆形框
	//Mat drawing = Mat::zeros( threshold_output.size(), CV_8UC3 );
	Mat drawing = g_srcImage.clone();
	for( int unsigned i = 0; i<contours.size( ); i++ )
	{
		Scalar color = Scalar( g_rng.uniform(0, 255), g_rng.uniform(0,255), g_rng.uniform(0,255) );//随机设置颜色
		drawContours( drawing, contours_poly, i, color, 1, 8, vector<Vec4i>(), 0, Point() );//绘制轮廓
		rectangle( drawing, boundRect[i].tl(), boundRect[i].br(), color, 2, 8, 0 );//绘制矩形
		circle( drawing, center[i], (int)radius[i], color, 2, 8, 0 );//绘制圆
	}

	// 显示效果图窗口
	namedWindow( WINDOW_NAME2, WINDOW_AUTOSIZE );
	imshow( WINDOW_NAME2, drawing );
}

//-----------------------------------【ShowHelpText( )函数】----------------------------------  
//      描述：输出一些帮助信息  
//----------------------------------------------------------------------------------------------  
static void ShowHelpText()  
{  
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第75个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");

	//输出一些帮助信息  
	printf("\n\n\n\t欢迎来到【创建包围轮廓的矩形和圆形边界框】示例程序~\n\n");  
	printf( "\n\n\t按键操作说明: \n\n"  
		"\t\t键盘按键【ESC】- 退出程序\n\n"  
		"\t\t滑动滚动条 - 改变阈值\n\n");  
}  
```

&emsp;&emsp;（二）显示结果

![Contour shape analysis experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment1.png)

![Contour shape analysis experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment2.png)

![Contour shape analysis experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment3.png)

![Contour shape analysis experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment4.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解轮廓形状分析的基本原理；掌握实现轮廓形状分析的代码编写方法。新建工程，在VS2015中配置OpenCV，得到原图的灰度图像并进行平滑，使用Threshold检测边缘，找出轮廓，多边形逼近轮廓，获取矩形和圆形边界框，绘制多边形轮廓、包围的矩形框和圆形框。