---
title: 计算机视觉 - 实验十五 对视频的快速角点检测实验
description: Computer Vision - Experiment 15 - Fast corner point detection experiments on video
date: '2020-06-10'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验十五 对视频的快速角点检测实验

### 实验目的和要求

&emsp;&emsp;理解角点检测的基本原理；掌握实现角点检测的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用VideoCapture类打开视频文件；

&emsp;&emsp;（四）读取视频中的一帧图像；

&emsp;&emsp;（五）转换灰度图并检测角点;

&emsp;&emsp;（六）遍历每个点，进行绘制，在原图中显示角点。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio2015。

### 实验原理

&emsp;&emsp;（一）角点检测是计算机视觉系统中用来获得图像特征的-种方法。角点通常被定义为两条边的交点，更严格地说法是，角点的局部邻域应该具有两个不同区域的不同方向的边界。而实际应用中，大多数所谓的角点检测方法检测的是拥有特定特征的图像点，而不仅仅是“角点”。这些特征点在图像中有具体的坐标，并具有某些数学特征，如局部最大或最小灰度等；

&emsp;&emsp;（二）角点被大量用于解决物体识别、图像识别、图像匹配、视觉跟踪、三维重建等一系列的问题。我们不再观察整幅图，而是选择某些特殊的点，然后对它们进行局部有的放矢地分析。如果能检测到足够多的这种点，同时它们的区分度很高，并且可以精确定位稳定的特征，那么这个方法就具有实用价值；

&emsp;&emsp;（三）角点检测方法的一个很重要的评价标准是其对多幅图像中相同或相似特征的检测能力，并且能够应对光照变化、图像旋转等图像变化。Shi-Tomasi算法是Harris算法的改进,本实验通过播放一段视频，展示对于视频中同一目标，Shi-Tomasi算法得到的角点具有很强的健壮性。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）调用VideoCapture类的open函数打开视频；

&emsp;&emsp;（四）调用VideoCapture类的“>>”方法读取视频中的一帧图像；

&emsp;&emsp;（五）调用cvtColor函数转换灰度图，调用goodFeaturesToTrack函数检测角点;

&emsp;&emsp;（六）遍历每个点，调用circle在原图中进行绘制角点。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）VideoCapture类的功能和使用方法；

&emsp;&emsp;（三）cvtColor函数的功能和使用方法；

&emsp;&emsp;（四）goodFeaturesToTrack函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/calib3d/calib3d.hpp"
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include "opencv2/features2d/features2d.hpp"
#include <iostream>
#include <list>
#include <vector>
using namespace std;
using namespace cv;
//---------------------------------【help( )函数】--------------------------------------
//		 描述：输出一些帮助信息
//-----------------------------------------------------------------------------------

int Harris(Mat &img)
{
	Mat grayImage;
	//转换灰度图
	cvtColor(img, grayImage, CV_BGR2GRAY);

	//开始进行角点检测  
	vector<Point2f> dstPoint2f;
	goodFeaturesToTrack(grayImage, dstPoint2f, 200, 0.01, 10, Mat(), 3);

	//遍历每个点，进行绘制，便于显示  
	//Mat dstImage;
	//img.copyTo(dstImage);
	for (int i = 0; i < (int)dstPoint2f.size(); i++)
	{
		circle(img, dstPoint2f[i], 3, Scalar(0,0,255), 2, 8);
	}
	return 0;
}
//---------------------------【main( )函数】--------------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main()
{
	VideoCapture capture;
	capture.open("1.avi");
	if (!capture.isOpened())
	{
		cout << "capture device " << " failed to open!" << endl;
		return 1;
	}
	Mat frame;
	Mat gray;
	for (;;)
	{
		capture >> frame;
		if (frame.empty())
			break;
		
		int h = frame.rows;
		int w = frame.cols;
		Harris(frame);
		imshow("frame", frame);
		waitKey(3);  //延时30ms
	}
	return 0;
} 
```

&emsp;&emsp;（二）显示结果

![Fast corner point detection experiments on video 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video1.png)

![Fast corner point detection experiments on video 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video2.png)

![Fast corner point detection experiments on video 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video3.png)

![Fast corner point detection experiments on video 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video4.png)

![Fast corner point detection experiments on video 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video5.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解角点检测的基本原理；掌握实现角点检测的代码编写方法。新建工程；在VS2015中配置OpenCV；使用VideoCapture类打开视频文件；读取视频中的一帧图像；转换灰度图并检测角点；遍历每个点，进行绘制，在原图中显示角点。