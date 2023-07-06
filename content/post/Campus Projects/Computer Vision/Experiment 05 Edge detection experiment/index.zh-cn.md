---
title: Computer Vision - Experiment 5 - Edge detection experiment
description: 计算机视觉 - 实验五 边缘检测实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验五 边缘检测实验

### 实验目的和要求

&emsp;&emsp;（一）通过实验掌握图像的canny边缘检测的原理和编程实现方法；

&emsp;&emsp;（二）通过实验掌握图像的sobel边缘检测的原理和编程实现方法；

&emsp;&emsp;（三）通过实验掌握图像的scharr滤波器的原理和编程实现方法。

### 实验内容

&emsp;&emsp;（一）使用OpenCV中的Canny函数实现边缘检测;

&emsp;&emsp;（二）使用OpenCV中的Sobel函数实现边缘检测;

&emsp;&emsp;（三）使用OpenCV中的Scharr函数实现边缘检测。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）最优边缘检测的三个主要评价标准。低错误率：标识出尽可能多的实际边缘，同时尽可能地减少噪声产生的误报；高定位性：标识出的边缘要与图像中的实际边缘尽可能接近；最小响应：图像中的边缘只能标识一次，并且可能存在的图像噪声不应标识为边缘。

&emsp;&emsp;（二）Canny边缘检测算子是John F.Canny于1986年开发出来的一个多级边缘检测算法。Canny 算法被推崇为当今最优的边缘检测的算法。

&emsp;&emsp;（三）Sobel算子是一个主要用于边缘检测的离散微分算子。它结合了高斯平滑和徽分求导，用来计算图像灰度函数的近似梯度。scharr一般称它为滤波器，而不是算子，它在OpenCV中主要是配合Sobel算子的运算而存在的。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用Canny函数实现边缘检测；

&emsp;&emsp;（四）编写代码，使用Sobel函数实现边缘检测；

&emsp;&emsp;（五）编写代码，使用Scharr函数实现边缘检测。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）Canny函数、Sobel函数、Scharr函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//--------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>
using namespace cv;


//--------------------------------【全局变量声明部分】-----------------------------------
//		描述：全局变量声明
//-------------------------------------------------------------------------------------
//原图，原图的灰度版，目标图
Mat g_srcImage, g_srcGrayImage,g_dstImage;

//Canny边缘检测相关变量
Mat g_cannyDetectedEdges;
int g_cannyLowThreshold=1;//TrackBar位置参数  

//Sobel边缘检测相关变量
Mat g_sobelGradient_X, g_sobelGradient_Y;
Mat g_sobelAbsGradient_X, g_sobelAbsGradient_Y;
int g_sobelKernelSize=1;//TrackBar位置参数  

//Scharr滤波器相关变量
Mat g_scharrGradient_X, g_scharrGradient_Y;
Mat g_scharrAbsGradient_X, g_scharrAbsGradient_Y;


//--------------------------------【全局函数声明部分】-----------------------------------
//		描述：全局函数声明
//-------------------------------------------------------------------------------------
static void ShowHelpText( );
static void on_Canny(int, void*);//Canny边缘检测窗口滚动条的回调函数
static void on_Sobel(int, void*);//Sobel边缘检测窗口滚动条的回调函数
void Scharr( );//封装了Scharr边缘检测相关代码的函数


//-------------------------------【main( )函数】-----------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main( int argc, char** argv )
{
	//改变console字体颜色
	system("color 2F");  

	//显示欢迎语
	ShowHelpText();

	//载入原图
	g_srcImage = imread("1.jpg");
	if( !g_srcImage.data ) { printf("Oh，no，读取srcImage错误~！ \n"); return false; }

	//显示原始图
	namedWindow("【原始图】");
	imshow("【原始图】", g_srcImage);

	// 创建与src同类型和大小的矩阵(dst)
	g_dstImage.create( g_srcImage.size(), g_srcImage.type() );

	// 将原图像转换为灰度图像
	cvtColor( g_srcImage, g_srcGrayImage, COLOR_BGR2GRAY );

	// 创建显示窗口
	namedWindow( "【效果图】Canny边缘检测", WINDOW_AUTOSIZE );
	namedWindow( "【效果图】Sobel边缘检测", WINDOW_AUTOSIZE );

	// 创建trackbar
	createTrackbar( "参数值：", "【效果图】Canny边缘检测", &g_cannyLowThreshold, 120, on_Canny );
	createTrackbar( "参数值：", "【效果图】Sobel边缘检测", &g_sobelKernelSize, 3, on_Sobel );

	// 调用回调函数
	on_Canny(0, 0);
	on_Sobel(0, 0);

	//调用封装了Scharr边缘检测代码的函数
	Scharr( );

	//轮询获取按键信息，若按下Q，程序退出
	while((char(waitKey(1)) != 'q')) {}

	return 0;
}


//--------------------------------【ShowHelpText( )函数】--------------------------------
//		描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
static void ShowHelpText()
{
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第60个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");

	//输出一些帮助信息
	printf( "\n\n\t运行成功，请调整滚动条观察图像效果~\n\n"
		"\t按下“q”键时，程序退出。\n");
}


//----------------------------------【on_Canny( )函数】----------------------------------
//		描述：Canny边缘检测窗口滚动条的回调函数
//-------------------------------------------------------------------------------------
void on_Canny(int, void*)
{
	// 先使用 3x3内核来降噪
	blur( g_srcGrayImage, g_cannyDetectedEdges, Size(3,3) );

	// 运行我们的Canny算子
	//void cvCanny(
	//	const CvArr* image,              //第一个参数表示输入图像，必须为单通道灰度图
	//	CvArr* edges,                      //第二个参数表示输出的边缘图像，为单通道黑白图
	//	double threshold1,
	//	double threshold2,               //第三个参数和第四个参数表示阈值，这二个阈值中当中的小阈值用来控制边缘连接，
	//	大的阈值用来控制强边缘的初始分割即如果一个像素的梯度大与上限值，则被认为
	//	是边缘像素，如果小于下限阈值，则被抛弃。如果该点的梯度在两者之间则当这个
	//	点与高于上限值的像素点连接时我们才保留，否则删除。
	//	int aperture_size = 3              //第五个参数表示Sobel 算子大小，默认为3即表示一个3*3的矩阵。Sobel 算子与
	//	高斯拉普拉斯算子都是常用的边缘算子
	//	);
	Canny( g_cannyDetectedEdges, g_cannyDetectedEdges, g_cannyLowThreshold, g_cannyLowThreshold*3, 3 );

	//先将g_dstImage内的所有元素设置为0 
	g_dstImage = Scalar::all(0);

	//使用Canny算子输出的边缘图g_cannyDetectedEdges作为掩码，来将原图g_srcImage拷到目标图g_dstImage中
	g_srcImage.copyTo( g_dstImage, g_cannyDetectedEdges);

	//显示效果图
	imshow( "【效果图】Canny边缘检测", g_dstImage );
	imshow( "g_cannyDetectedEdges", g_cannyDetectedEdges);
}



//----------------------------------【on_Sobel( )函数】----------------------------------
//		描述：Sobel边缘检测窗口滚动条的回调函数
//-------------------------------------------------------------------------------------
void on_Sobel(int, void*)
{
	// 求 X方向梯度
	//void Sobel(InputArray src, OutputArray dst, int ddepth,
	//	int dx, int dy, int ksize = 3,
	//第四个参数，int类型dx，x 方向上的差分阶数。
	//第五个参数，int类型dy，y方向上的差分阶数。
	Sobel( g_srcImage, g_sobelGradient_X, CV_16S, 1, 0, (2*g_sobelKernelSize+1));
	convertScaleAbs( g_sobelGradient_X, g_sobelAbsGradient_X );//计算绝对值，并将结果转换成8位
																   //显示效果图
	imshow("【效果图】Sobel边缘检测x", g_sobelAbsGradient_X);

	// 求Y方向梯度
	Sobel( g_srcImage, g_sobelGradient_Y, CV_16S, 0, 1, (2*g_sobelKernelSize+1));
	convertScaleAbs( g_sobelGradient_Y, g_sobelAbsGradient_Y );//计算绝对值，并将结果转换成8位
	imshow("【效果图】Sobel边缘检测y", g_sobelAbsGradient_Y);

	// 合并梯度
	//void addWeighted(InputArray src1, double alpha, InputArray src2,
	//	double beta, double gamma, OutputArray dst, int dtype = -1);
	//dst = src1*alpha + src2*beta + gamma;
	addWeighted( g_sobelAbsGradient_X, 0.5, g_sobelAbsGradient_Y, 0.5, 0, g_dstImage );

	//显示效果图
	imshow("【效果图】Sobel边缘检测", g_dstImage); 

}


//-----------------------------------【Scharr( )函数】----------------------------------
//		描述：封装了Scharr边缘检测相关代码的函数
//-------------------------------------------------------------------------------------
void Scharr( )
{
	// 求 X方向梯度
	Scharr( g_srcImage, g_scharrGradient_X, CV_16S, 1, 0);
	//void convertScaleAbs(InputArray src, OutputArray dst,
	//	double alpha = 1, double beta = 0);
	//先缩放元素再取绝对值，最后转换格式为8bit型
	convertScaleAbs( g_scharrGradient_X, g_scharrAbsGradient_X );//计算绝对值，并将结果转换成8位
	//显示效果图
	imshow("【效果图】Scharr滤波器x", g_scharrAbsGradient_X);
	// 求Y方向梯度
	Scharr( g_srcImage, g_scharrGradient_Y, CV_16S, 0, 1);
	convertScaleAbs( g_scharrGradient_Y, g_scharrAbsGradient_Y );//计算绝对值，并将结果转换成8位
	imshow("【效果图】Scharr滤波器y", g_scharrAbsGradient_Y);

	// 合并梯度
	addWeighted( g_scharrAbsGradient_X, 0.5, g_scharrAbsGradient_Y, 0.5, 0, g_dstImage );

	//显示效果图
	imshow("【效果图】Scharr滤波器", g_dstImage); 
}
```

&emsp;&emsp;（二）显示结果

![Edge detection experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment1.png)

![Edge detection experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment2.png)

![Edge detection experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment3.png)

![Edge detection experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment4.png)

![Edge detection experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment5.png)

![Edge detection experiment 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment6.png)

![Edge detection experiment 7](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment7.png)

![Edge detection experiment 8](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment8.png)

![Edge detection experiment 9](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment9.png)

![Edge detection experiment 10](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment10.png)

![Edge detection experiment 11](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2005%20Edge%20detection%20experiment/edge-detection-experiment11.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是掌握图像的canny边缘检测的原理和编程实现方法、掌握图像的sobel边缘检测的原理和编程实现方法、掌握图像的scharr滤波器的原理和编程实现方法。使用OpenCV中的Canny函数实现边缘检测、使用OpenCV中的Sobel函数实现边缘检测、使用OpenCV中的Scharr函数实现边缘检测。通过编写代码，我学会了使用Canny函数、Sobel函数和Scharr函数实现边缘检测。
