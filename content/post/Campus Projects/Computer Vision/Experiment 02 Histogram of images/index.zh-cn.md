---
title: Computer Vision - Experiment 2 - Histogram of images
description: 计算机视觉 - 实验二 图像的直方图
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验二 图像的直方图

### 实验目的和要求

&emsp;&emsp;（一）通过实验掌握绘制图像的直方图方法；

&emsp;&emsp;（二）通过实验掌握图像直方图均衡化方法。

### 实验内容

&emsp;&emsp;（一）使用OpenCV中的calcHist函数计算直方图，计算完成之后，采用OpenCV中的rectangle函数绘制矩形来完成直方图绘制;

&emsp;&emsp;（二）在OpenCV中，使用equalizeHist函数实现直方图均衡化的功能。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows 7 操作系统和 Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）直方图的计算在OpenCV中可以使用calcHist函数，而计算完成之后，可以采用 OpenCV中的绘图函数，如绘制矩形的rectangle函数来完成;

&emsp;&emsp;（二）很多时候，用相机拍摄的照片的效果往往会不尽人意。这时可以对这些图像进行一些处理，来扩大图像的动态范围。这种情况下最常用到的技术就是直方图均衡化，经过均衡化的图像，其频谱更加舒展，有效地利用了0-255的空间，图像表现力更加出色；在OpenCV 中，直方图均衡化的功能实现由equalizeHist函数完成。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用calcHist函数和rectangle绘制图像直方图；

&emsp;&emsp;（四）编写代码，使用equalizeHist函数完成直方图均衡化。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）calcHist、equalizeHist函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//------------------------------【头文件、命名空间包含部分】---------------------------
//          描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
using namespace cv;
//-----------------------------------【main( )函数】-------------------------------------
//          描述：控制台应用程序的入口函数，我们的程序从这里开始执行
//-------------------------------------------------------------------------------------
Mat drawHist(Mat srcImage)
{
	//【2】定义变量
	MatND dstHist;       // 在cv中用CvHistogram *hist = cvCreateHist
	int dims = 1;
	float hranges[] = { 0, 255 };
	const float *ranges[] = { hranges };   // 这里需要为const类型
	int size = 256; //设定bin数目，必须和灰度级数目相等，这里是0到255，所以size为256
	int channels = 0;
	//【3】计算图像的直方图
	//void calcHist(const Mat* images, int nimages,
	//	const int* channels, InputArray mask,
	//	OutputArray hist, int dims, const int* histSize,
	//	const float** ranges, bool uniform = true, bool accumulate = false)
	//参数1表示需要用来计算直方图的源图像序列，因此可以允许有多张大小一样，数据类型相同的图像被用来统计其直方图特征。
	//参数2表示的就是使用多少张图像序列中的图像用于计算直方图。
	//参数3的出现主要是考虑到输入的每一张图像有可能是多通道的，比如说RGB图就是3通道的，那么从统计意义上来讲，一张RGB图其实就是3张单通道的图像，而计算直方图时其本质也是针对单张图像进行的。这里虽然我们输入的图像序列images中有很多图片，但是并不是每一张图片的每一个通道都会被用来计算。所以参数3的功能是指定哪些通道的图像被用来计算（后面的解释都假设图像序列中图像是3通道的，那么有的图像可能有多个通道都被用来计算，有的图像可能连一个通道都没有被采用），这时参数3里面保存的是通道的序号，那么图像序列images中的第一张图片的通道序号（假设图像时3通道的）为0, 1, 2；images中第二张图片的图像序列接着上一次的，为3, 4, 5, ；依次类推即可。
	//参数4是mask掩膜操作，即指定每张图片的哪些像素被用于计算直方图，这个掩膜矩阵不能够针对特定图像设定特定的掩膜，因此在这里是一视同仁对待的。
	//参数5是保存计算的直方图结果的矩阵，有可能是多维矩阵。
	//参数6是需要计算的直方图的维数。
	//参数7是所需计算直方图的每一维的大小，即每一维bin的个数。
	calcHist(&srcImage, 1, &channels, Mat(), dstHist, dims, &size, ranges);    // cv 中是cvCalcHist
	int scale = 1;
	Mat dstImage(size * scale, size, CV_8U, Scalar(0));
	//【4】获取最大值和最小值
	double minValue = 0;
	double maxValue = 0;
	minMaxLoc(dstHist, &minValue, &maxValue, 0, 0);  //  在cv中用的是cvGetMinMaxHistValue
	//【5】绘制出直方图
	//saturate_cast<int>(double v)           { return cvRound(v); }
	int hpt = saturate_cast<int>(0.9 * size);//防止溢出,hpt=230
	for (int i = 0; i < 256; i++)
	{
		float binValue = dstHist.at<float>(i);           //   注意hist中是float类型    而在OpenCV1.0版中用cvQueryHistValue_1D
		int realValue = saturate_cast<int>(binValue * hpt / maxValue);
		rectangle(dstImage, Point(i*scale, size - 1), Point((i + 1)*scale - 1, size - realValue), Scalar(255));
	}
	return dstImage;
}
int main()
{
	// 【1】加载源图像
	Mat srcImage, dstImage;
	srcImage = imread("1.jpg", 1);
	if (!srcImage.data) { printf("读取图片错误，请确定目录下是否有imread函数指定图片存在~！ \n"); return false; }
	// 【2】转为灰度图并显示出来
	cvtColor(srcImage, srcImage, COLOR_BGR2GRAY);
	imshow("原始图", srcImage);
	Mat histSrc = drawHist(srcImage);
	imshow("histSrc", histSrc);
	// 【3】进行直方图均衡化
	equalizeHist(srcImage, dstImage);
	Mat histDst = drawHist(dstImage);
	imshow("histDst", histDst);
	// 【4】显示结果
	imshow("经过直方图均衡化后的图", dstImage);
	// 等待用户按键退出程序
	waitKey(0);
	return 0;
}
```

&emsp;&emsp;（二）显示结果

![Histogram of images 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2002%20Histogram%20of%20images/histogram-of-image1.png)

![Histogram of images 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2002%20Histogram%20of%20images/histogram-of-image2.png)

![Histogram of images 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2002%20Histogram%20of%20images/histogram-of-image3.png)

![Histogram of images 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2002%20Histogram%20of%20images/histogram-of-image4.png)

![Histogram of images 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2002%20Histogram%20of%20images/histogram-of-image5.png)

![Histogram of images 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2002%20Histogram%20of%20images/histogram-of-image6.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是掌握绘制图像的直方图方法和图像直方图均衡化方法。使用OpenCV中的calcHist函数计算直方图，计算完成之后，采用 OpenCV中的rectangle函数绘制矩形来完成直方图绘制; 在OpenCV中，使用equalizeHist函数实现直方图均衡化的功能。通过编写代码，我学会了使用calcHist函数和rectangle绘制图像直方图；学会了使用equalizeHist函数完成直方图均衡化。
