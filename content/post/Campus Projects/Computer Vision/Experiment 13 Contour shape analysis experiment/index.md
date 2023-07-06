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

## Computer Vision - Experiment 13 - Contour shape analysis experiment

### Experimental objectives and requirements

&emsp;&emsp;To understand the basic principles of contour shape analysis; to master the method of writing code to implement contour shape analysis.

### Experiment content

&emsp;&emsp; (i) New project.

&emsp;&emsp; (ii) Configure OpenCV in VS2015.

&emsp;&emsp; (iii) Obtain the grayscale image of the original image and smooth it;

&emsp;&emsp; (iv) Detecting edges using Threshold;

&emsp;&emsp; (v) Find the contours.

&emsp;&emsp; (vi) polygonal approximation of contours and obtaining rectangular and circular bounding boxes;

&emsp;&emsp; (vii) Draw polygonal outlines, enclosing rectangular and circular boxes.

### Experimental apparatus, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed.

### Experimental principle

&emsp;&emsp; (i) In computer vision, shape features are an important means to describe high-level visual features (e.g., target, object). The target, object is especially important to obtain the semantics of the image, so it is necessary to have good algorithms for the extraction and description of shape features. Contour shape analysis is an important way to extract shape features.

&emsp;&emsp; (ii) This experiment first finds the target contour, then approximates the polygon curve with specified accuracy, then calculates the outermost rectangular boundary of the point set, finds the enclosing circle with minimum area, and finally draws the polygon contour, enclosing rectangular box, and circular box, and compares the effect of the three extracted contour shapes on the description of the target object.

### Experimental steps

&emsp;&emsp; (i) Create the Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Obtain the grayscale image of the original image and smooth it;

&emsp;&emsp; (iv) Binarize using the threshold function in OpenCV;

&emsp;&emsp; (v) Use the findContours function in OpenCV to find the contours.

&emsp;&emsp; (vi) polygon approximation of contours using the approxPolyDP function in OpenCV, rectangle acquisition using the boundingRect function in OpenCV, and circular bounding box using the minEnclosingCircle function in OpenCV;

&emsp;&emsp; (vii) Draw polygon outlines using the drawContours function in OpenCV, enclosing rectangle boxes using the rectangle function in OpenCV, and enclosing circle boxes using the circle function in OpenCV.

### Experimental Notes

&emsp;&emsp; (i) The method of configuring OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of the threshold function;

&emsp;&emsp; (iii) The functions and usage of the approxPolyDP function;

&emsp;&emsp; (iv) the functions and usage of the rectangle function.

### Experimental results

&emsp;&emsp; (i) Experimental code

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

&emsp;&emsp; (ii) Show results

![Contour shape analysis experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment1.png)

![Contour shape analysis experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment2.png)

![Contour shape analysis experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment3.png)

![Contour shape analysis experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2013%20Contour%20shape%20analysis%20experiment/contour-shape-analysis-experiment4.png)

### Experiment summary

&emsp;&emsp;The main content of this experiment is to understand the basic principle of contour shape analysis; master the code writing method to implement contour shape analysis. Create a new project, configure OpenCV in VS2015, get the grayscale image of the original image and smooth it, use Threshold to detect the edges, find out the contour, polygon approximation of the contour, get the rectangular and circular bounding boxes, draw the polygon contour, the enclosed rectangular box and the circular box.