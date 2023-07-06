---
title: Computer Vision - Experiment 3 - Image linear filtering experiment
description: 计算机视觉 - 实验三 图像线性滤波实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 3 - Image linear filtering experiment

### Experimental objectives and requirements

&emsp;&emsp; (i) To master the principle of box filtering of images and the programming implementation method through experiments; 

&emsp;&emsp; (ii) To master the principle of mean filtering of images and the programmed implementation method through experiments;

&emsp;&emsp; (ii) To master the principle of Gaussian filtering of images and the programmed implementation method through experiments.

### Experiment content

&emsp;&emsp; (i) Use the boxFilter function in OpenCV to implement box filtering.

&emsp;&emsp; (ii) Implementing mean filtering using the blur function in OpenCV;

&emsp;&emsp; (iii) Gaussian filtering using GaussianBlur function in OpenCV.  

### Experimental instruments, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed 

### Experimental principle

&emsp;&emsp; (i) Image filtering, which refers to the suppression of noise in the target image under the condition of preserving as much as possible the detailed features of the image, is an indispensable operation in image pre-processing, and the effectiveness of its processing will directly affect the validity and reliability of subsequent image processing and analysis. The output value of each pixel of the linear filter is the weighted sum of some input pixels. Linear filters are easy to construct, well and easy to analyze from a frequency response perspective. 

&emsp;&emsp; (ii) In OpenCV, the following three commonly used linear filter operations are provided, which are encapsulated in separate functions and are very easy to use: boxFilter function, mean filter blur function; Gaussian filter GaussianBlur function. 

### Experimental steps

&emsp;&emsp; (i) Create the Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Write code to implement box filtering using the boxFilter function;

&emsp;&emsp; (iv) Write code to implement mean filtering using the blur function;

&emsp;&emsp; (v) Write code to implement Gaussian filtering using the gaussianBlur function.

### Experimental notes

&emsp;&emsp; (i) Configure OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of boxFilter function, blur function and gaussianBlur function.

### Experimental results

&emsp;&emsp; (i) Experimental code

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

&emsp;&emsp; (ii) Show results

![Image linear filtering experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment1.png)

![Image linear filtering experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment2.png)

![Image linear filtering experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment3.png)

![Image linear filtering experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment4.png)

![Image linear filtering experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment5.png)

![Image linear filtering experiment 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2003%20Image%20linear%20filtering%20experiment/image-linear-filtering-experiment6.png)

### Experiment summary

&emsp;&emsp;The main content of this experiment is to master the principle of box filtering and programming implementation method of image, master the principle of mean filtering and programming implementation method of image, master the principle of Gaussian filtering and programming implementation method of image. I used the boxFilter function in OpenCV to implement box filtering, the blur function in OpenCV to implement mean filtering, and the GaussianBlur function in OpenCV to implement Gaussian filtering. By writing code, I learned to implement box filtering, mean filtering and Gaussian filtering using the boxFilter function, blur function and GaussianBlur function.
