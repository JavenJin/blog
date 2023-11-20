---
title: 计算机视觉 - 实验八 图像分割实验
description: Computer Vision - Experiment 8 - Image segmentation experiment
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验八 图像分割实验

### 实验目的和要求

&emsp;&emsp;理解使用meanShfit进行图像分割的基本原理；掌握使用OpenCV通过均值漂移算法实现彩色图像分割的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用OpenCV中的pyrMeanShiftFiltering函数实现彩色图像分割；

&emsp;&emsp;（四）使用OpenCV中的floodFill函数对其分割的结果用不同的颜色进行填充。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）meanShfit（均值漂移）算法是一种通用的聚类算法，它的基本原理是：对于给定的一定数量样本，任选其中一个样本，以该样本为中心点划定一个圆形区域，求取该圆形区域内样本的质心，即密度最大处的点，再以该点为中心继续执行上述迭代过程，直至最终收敛。

&emsp;&emsp;（二）meanShfit不仅可以用于图像滤波，视频跟踪，还可以用于图像分割。可以利用均值漂移的算法特性，实现彩色图像分割。Opencv中对应的函数是pyrMeanShiftFiltering。pyrMeanShiftFiltering是图像在色彩层面的平滑滤波，它可以中和色彩分布相近的颜色，平滑色彩细节，侵蚀掉面积较小的颜色区域，从而实现分割效果。

&emsp;&emsp;（三）本实验的主要过程是，首先设置好参数，然后用函数pyrMeanShiftFiltering函数对输入的图像进行分割。分割后的结果保存在该函数的第二个参数即输出图像中，最后根据该分割图像的特点用floodFill函数对其分割的结果用不同的颜色进行填充。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用pyrMeanShiftFiltering函数实现彩色图像分割；

&emsp;&emsp;（四）编写代码，使用floodFill函数对其分割的结果用不同的颜色进行填充。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）pyrMeanShiftFiltering函数的功能和使用方法；

&emsp;&emsp;（三）floodFill函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//-------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/core/core.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include <iostream>
using namespace cv;
using namespace std;


//---------------------------------【help( )函数】--------------------------------------
//		 描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
static void help()
{
	cout << "\n\t此程序演示了OpenCV中MeanShift图像分割的使用。\n"
		<< "\n\t程序运行后我们可以通过3个滑动条调节分割效果。调节滑动条后可能会有些许卡顿，请耐心等待\n"
		<< "\n\t3个滑动条代表的参数分别为空间窗的半径 （spatialRad）、色彩窗的半径（colorRad）、最大图像金字塔级别（maxPyrLevel）\n"
		<< endl;
}


//This colors the segmentations
static void floodFillPostprocess( Mat& img, const Scalar& colorDiff=Scalar::all(1) )
{
	CV_Assert( !img.empty() );
	RNG rng = theRNG();
	Mat mask( img.rows+2, img.cols+2, CV_8UC1, Scalar::all(0) );
	for( int y = 0; y < img.rows; y++ )
	{
		for( int x = 0; x < img.cols; x++ )
		{
			if( mask.at<uchar>(y+1, x+1) == 0 )
			{
				Scalar newVal( rng(256), rng(256), rng(256) );
				floodFill( img, mask, Point(x,y), newVal, 0, colorDiff, colorDiff );
			}
		}
	}
}

string winName = "meanshift";
int spatialRad, colorRad, maxPyrLevel;
Mat img, res;



static void meanShiftSegmentation( int, void* )
{
	cout << "spatialRad=" << spatialRad << "; "
		<< "colorRad=" << colorRad << "; "
		<< "maxPyrLevel=" << maxPyrLevel << endl;
	pyrMeanShiftFiltering( img, res, spatialRad, colorRad, maxPyrLevel );
	floodFillPostprocess( res, Scalar::all(2) );
	imshow( winName, res );
}



//--------------------------【main( )函数】--------------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//------------------------------------------------------------------------------------
int main(int argc, char** argv)
{

	help();

	img = imread( "1.jpg" );
	if( img.empty() )
		return -1;
	imshow("原始图",img);
	spatialRad = 10;
	colorRad = 10;
	maxPyrLevel = 1;

	namedWindow( winName, WINDOW_AUTOSIZE );

	createTrackbar( "spatialRad", winName, &spatialRad, 80, meanShiftSegmentation );
	createTrackbar( "colorRad", winName, &colorRad, 60, meanShiftSegmentation );
	createTrackbar( "maxPyrLevel", winName, &maxPyrLevel, 5, meanShiftSegmentation );

	meanShiftSegmentation(0, 0);
	waitKey();
	return 0;
}
```

&emsp;&emsp;（二）显示结果

![Image segmentation experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet1.png)

![Image segmentation experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet2.png)

![Image segmentation experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet3.png)

![Image segmentation experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet4.png)

![Image segmentation experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet5.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解使用meanShfit进行图像分割的基本原理；掌握使用OpenCV通过均值漂移算法实现彩色图像分割的代码编写方法。新建工程，在VS2015中配置OpenCV，使用OpenCV中的pyrMeanShiftFiltering函数实现彩色图像分割；使用OpenCV中的floodFill函数对其分割的结果用不同的颜色进行填充。学会了用pyrMeanShiftFiltering函数实现彩色图像分割；floodFill函数对其分割的结果用不同的颜色进行填充。