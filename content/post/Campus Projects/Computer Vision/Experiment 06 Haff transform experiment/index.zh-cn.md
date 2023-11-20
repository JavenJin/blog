---
title: 计算机视觉 - 实验六 哈夫变换实验
description: Computer Vision - Experiment 6 - Haff transform experiment
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验六 哈夫变换实验

### 实验目的和要求

&emsp;&emsp;理解哈夫变换的基本原理；掌握使用OpenCV实现哈夫变换的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用OpenCV中的函数实现哈夫变换检测线段。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）在图像处理和计算机视觉领域中，如何从当前的图像提取所需要的特征信息是图像识别的关键所在。在许多应用场什中需要快速准确地检测出直线或者圆，其中一种非常有效的解决问题的方法是哈夫变换。

&emsp;&emsp;（二）哈夫线变换是一种用来寻找直线的方法，在使用哈夫线变换之前，首先要对图像进行边缘检测的处理，即哈夫线变换的直接输入只能是边缘二值图像。

&emsp;&emsp;（三）在OpenCV中，可以用HoughLines函数来调用标准哈夫变换和多尺度哈夫变换。而HoughLinesP函数用于调用累计概率霍夫变换。累计概率霍夫变换执行效率很高，相比于HoughLines函数，我们更倾向于使用HoughLinesP函数。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用HoughLines或者HoughLinesP函数实现哈夫线变换检测线段。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）HoughLines或者HoughLinesP函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//--------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include <opencv2/opencv.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>
using namespace std;
using namespace cv;


//--------------------------------【全局变量声明部分】-----------------------------------
//		描述：全局变量声明
//-------------------------------------------------------------------------------------
Mat g_srcImage, g_dstImage,g_midImage;//原始图、中间图和效果图
vector<Vec4i> g_lines;//定义一个矢量结构g_lines用于存放得到的线段矢量集合
//变量接收的TrackBar位置参数
int g_nthreshold=100;

//--------------------------------【全局函数声明部分】-----------------------------------
//		描述：全局函数声明
//-------------------------------------------------------------------------------------

static void on_HoughLines(int, void*);//回调函数
static void ShowHelpText();


//-------------------------------【main( )函数】-----------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main( )
{
	//改变console字体颜色
	system("color 4F");  

	ShowHelpText();

	//载入原始图和Mat变量定义   
	Mat g_srcImage = imread("1.jpg");  //工程目录下应该有一张名为1.jpg的素材图

	//显示原始图  
	imshow("【原始图】", g_srcImage);  

	//创建滚动条
	namedWindow("【效果图】",1);
	createTrackbar("值", "【效果图】",&g_nthreshold,200,on_HoughLines);

	//进行边缘检测和转化为灰度图
	Canny(g_srcImage, g_midImage, 50, 200, 3);//进行一次canny边缘检测
	imshow("canny", g_midImage);
	cvtColor(g_midImage,g_dstImage, COLOR_GRAY2BGR);//转化边缘检测后的图为灰度图

	//调用一次回调函数，调用一次HoughLinesP函数
	on_HoughLines(g_nthreshold,0);
	HoughLinesP(g_midImage, g_lines, 1, CV_PI/180, 80, 50, 10 );
	

	//显示效果图  
	imshow("【效果图】", g_dstImage);  


	waitKey(0);  

	return 0;  

}


//---------------------------------【on_HoughLines( )函数】------------------------------
//		描述：【顶帽运算/黑帽运算】窗口的回调函数
//-------------------------------------------------------------------------------------
static void on_HoughLines(int, void*)
{
	//定义局部变量储存全局变量
	Mat dstImage=g_dstImage.clone();
	Mat midImage=g_midImage.clone();

	//调用HoughLinesP函数
	//CV_EXPORTS_W void HoughLinesP(InputArray image, OutputArray lines,
	//	double rho, double theta, int threshold,
	//	double minLineLength = 0, double maxLineGap = 0);
	//image： 必须是二值图像，推荐使用canny边缘检测的结果图像； 
	//rho: 线段以像素为单位的距离精度，double类型的，推荐用1.0
	//theta： 线段以弧度为单位的角度精度，推荐用numpy.pi / 180
	//threshod : 累加平面的阈值参数，int类型，超过设定阈值才被检测出线段，值越大，基本上意味着检出的线段越长，检出的线段个数越少。根据情况推荐先用100试试
	//lines：这个参数的意义未知，发现不同的lines对结果没影响，但是不要忽略了它的存在 
	//minLineLength：线段以像素为单位的最小长度，根据应用场景设置 
	//maxLineGap：同一方向上两条线段判定为一条线段的最大允许间隔（断裂），超过了设定值，则把两条线段当成一条线段，值越大，允许线段上的断裂越大，越有可能检出潜在的直线段

	vector<Vec4i> mylines;
	HoughLinesP(midImage, mylines, 1, CV_PI/180, g_nthreshold+1, 50, 10 );

	//循环遍历绘制每一条线段
	for( size_t i = 0; i < mylines.size(); i++ )
	{
		Vec4i l = mylines[i];
		line( dstImage, Point(l[0], l[1]), Point(l[2], l[3]), Scalar(23,180,55), 1, LINE_AA);
	}
	//显示图像
	imshow("【效果图】",dstImage);
}

//--------------------------------【ShowHelpText( )函数】--------------------------------
//		描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
static void ShowHelpText()
{
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第64个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");

	//输出一些帮助信息
	printf("\n\n\n\t请调整滚动条观察图像效果~\n\n");
} 
```

&emsp;&emsp;（二）显示结果

![Haff transform experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2006%20Haff%20transform%20experiment/haff-transform-experiment1.png)

![Haff transform experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2006%20Haff%20transform%20experiment/haff-transform-experiment2.png)

![Haff transform experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2006%20Haff%20transform%20experiment/haff-transform-experiment3.png)

![Haff transform experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2006%20Haff%20transform%20experiment/haff-transform-experiment4.png)

![Haff transform experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2006%20Haff%20transform%20experiment/haff-transform-experiment5.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解哈夫变换的基本原理；掌握使用OpenCV实现哈夫变换的代码编写方法。新建工程，在VS2015中配置OpenCV，使用OpenCV中的函数实现哈夫变换检测线段。使用HoughLines函数来调用标准哈夫变换和多尺度哈夫变换，HoughLinesP函数用于调用累计概率霍夫变换。通过编写代码，我学会了使用HoughLines函数来调用标准哈夫变换和多尺度哈夫变换，使用HoughLinesP函数来调用累计概率霍夫变换。
