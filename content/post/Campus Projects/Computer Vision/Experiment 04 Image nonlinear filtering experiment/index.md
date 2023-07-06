---
title: Computer Vision - Experiment 4 - Image nonlinear filtering experiment
description: 计算机视觉 - 实验四 图像非线性滤波实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 4 - Image nonlinear filtering experiment

### Experimental objectives and requirements

&emsp;&emsp; (i) To master the principle of median filtering of images and the programming implementation method through experiments;

&emsp;&emsp; (ii) To master the principle of bilateral filtering of images and the programmed implementation method through experiments.

### Experiment content

&emsp;&emsp; (i) Implement median filtering using the medianBlur function in OpenCV.

&emsp;&emsp; (ii) Implement bilateral filtering using the bilateralFilter function in OpenCV.

### Experimental instruments, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed 

### Experimental principle

&emsp;&emsp; (i) image filtering, which refers to the suppression of noise in the target image under the condition of preserving as much as possible the detailed features of the image, is an indispensable operation in image pre-processing, and the effectiveness of its processing will directly affect the effectiveness and reliability of subsequent image processing and analysis.

&emsp;&emsp; (ii) In many cases, it is necessary to use the nonlinear filtering of neighboring pixels to get better results. For example, if the noise is scattered noise instead of Gaussian noise, i.e., when the image occasionally has very large values, the noise pixels are not removed if the image is blurred with a Gaussian filter; they are simply converted to softer but still visible scattered particles. A better result can be achieved at this point by using median filtering.

&emsp;&emsp; (iii) Bilateral filtering is a nonlinear filtering method that is an eclectic process that combines the spatial proximity of the image and the similarity of pixel values, taking into account both space domain information and grayscale similarity, to achieve edge-preserving denoising with simple, local characteristics.

&emsp;&emsp; (iv) In OpenCV, median filtering is implemented using the medianBlur function and bilateral filtering is implemented using the bilateralFilter function.

### Experimental steps

&emsp;&emsp; (i) Create a Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Write code to implement median filtering using the medianBlur function;

&emsp;&emsp; (iv) Use the bilateralFilter function to implement bilateral filtering.

### Experimental Notes

&emsp;&emsp; (i) The method of configuring OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of medianBlur function and bilateralFilter function.

### Experimental results

&emsp;&emsp; (i) Experimental code

```cpp
//---------------------------------【头文件包含部分】------------------------------------
//		描述：包含程序所依赖的头文件
//-------------------------------------------------------------------------------------
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>
#include <iostream>

//--------------------------------【命名空间声明部分】-----------------------------------
//		描述：包含程序所使用的命名空间
//-------------------------------------------------------------------------------------
using namespace std;
using namespace cv;


//---------------------------------【全局变量声明部分】----------------------------------
//		描述：全局变量声明
//-------------------------------------------------------------------------------------
Mat g_srcImage,g_dstImage1,g_dstImage2,g_dstImage3,g_dstImage4,g_dstImage5;
int g_nBoxFilterValue=6;  //方框滤波内核值
int g_nMeanBlurValue=10;  //均值滤波内核值
int g_nGaussianBlurValue=6;  //高斯滤波内核值
int g_nMedianBlurValue=10;  //中值滤波参数值
int g_nBilateralFilterValue=10;  //双边滤波参数值


//--------------------------------【全局函数声明部分】-----------------------------------
//		描述：全局函数声明
//-------------------------------------------------------------------------------------
//轨迹条回调函数
static void on_BoxFilter(int, void *);		//方框滤波
static void on_MeanBlur(int, void *);		//均值块滤波器
static void on_GaussianBlur(int, void *);			//高斯滤波器
static void on_MedianBlur(int, void *);			//中值滤波器
static void on_BilateralFilter(int, void *);			//双边滤波器
void ShowHelpText();


//--------------------------------【main( )函数】----------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main(   )
{
	system("color 4F");  

	ShowHelpText();	

	// 载入原图
	g_srcImage = imread( "20170829110313260.png", 1 );
	if( !g_srcImage.data ) { printf("读取srcImage错误~！ \n"); return false; }

	//克隆原图到5个Mat类型中
	g_dstImage1 = g_srcImage.clone( );
	g_dstImage2 = g_srcImage.clone( );
	g_dstImage3 = g_srcImage.clone( );
	g_dstImage4 = g_srcImage.clone( );
	g_dstImage5 = g_srcImage.clone( );

	//显示原图
	namedWindow("【<0>原图窗口】", 1);
	imshow("【<0>原图窗口】",g_srcImage);


	//=================【<1>方框滤波】=========================
	//创建窗口
	namedWindow("【<1>方框滤波】", 1);
	//创建轨迹条
	createTrackbar("内核值：", "【<1>方框滤波】",&g_nBoxFilterValue, 50,on_BoxFilter );
	on_MeanBlur(g_nBoxFilterValue,0);
	imshow("【<1>方框滤波】", g_dstImage1);
	//=====================================================


	//=================【<2>均值滤波】==========================
	//创建窗口
	namedWindow("【<2>均值滤波】", 1);
	//创建轨迹条
	createTrackbar("内核值：", "【<2>均值滤波】",&g_nMeanBlurValue, 50,on_MeanBlur );
	on_MeanBlur(g_nMeanBlurValue,0);
	//======================================================


	//=================【<3>高斯滤波】===========================
	//创建窗口
	namedWindow("【<3>高斯滤波】", 1);
	//创建轨迹条
	createTrackbar("内核值：", "【<3>高斯滤波】",&g_nGaussianBlurValue, 50,on_GaussianBlur );
	on_GaussianBlur(g_nGaussianBlurValue,0);
	//=======================================================


	//=================【<4>中值滤波】===========================
	//创建窗口
	namedWindow("【<4>中值滤波】", 1);
	//创建轨迹条
	createTrackbar("参数值：", "【<4>中值滤波】",&g_nMedianBlurValue, 50,on_MedianBlur );
	on_MedianBlur(g_nMedianBlurValue,0);
	//=======================================================


	//=================【<5>双边滤波】===========================
	//创建窗口
	namedWindow("【<5>双边滤波】", 1);
	//创建轨迹条
	createTrackbar("参数值：", "【<5>双边滤波】",&g_nBilateralFilterValue, 50,on_BilateralFilter);
	on_BilateralFilter(g_nBilateralFilterValue,0);
	//=======================================================


	//输出一些帮助信息
	cout<<endl<<"\t运行成功，请调整滚动条观察图像效果~\n\n"
		<<"\t按下“q”键时，程序退出。\n";
	while(char(waitKey(1)) != 'q') {}

	return 0;
}

//-----------------------------【on_BoxFilter( )函数】----------------------------------
//		描述：方框滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_BoxFilter(int, void *)
{
	//方框滤波操作
	boxFilter( g_srcImage, g_dstImage1, -1,Size( g_nBoxFilterValue+1, g_nBoxFilterValue+1));
	//显示窗口
	imshow("【<1>方框滤波】", g_dstImage1);
}

//-----------------------------【on_MeanBlur( )函数】------------------------------------
//		描述：均值滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_MeanBlur(int, void *)
{
	blur( g_srcImage, g_dstImage2, Size( g_nMeanBlurValue+1, g_nMeanBlurValue+1), Point(-1,-1));
	imshow("【<2>均值滤波】", g_dstImage2);

}

//----------------------------【on_GaussianBlur( )函数】---------------------------------
//		描述：高斯滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_GaussianBlur(int, void *)
{
	GaussianBlur( g_srcImage, g_dstImage3, Size( g_nGaussianBlurValue*2+1, g_nGaussianBlurValue*2+1 ), 0, 0);
	imshow("【<3>高斯滤波】", g_dstImage3);
}


//-----------------------------【on_MedianBlur( )函数】---------------------------------
//		描述：中值滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_MedianBlur(int, void *)
{
	medianBlur ( g_srcImage, g_dstImage4, g_nMedianBlurValue*2+1 );
	imshow("【<4>中值滤波】", g_dstImage4);
}


//-------------------------【on_BilateralFilter( )函数】---------------------------------
//		描述：双边滤波操作的回调函数
//-------------------------------------------------------------------------------------
static void on_BilateralFilter(int, void *)
{
	bilateralFilter ( g_srcImage, g_dstImage5, g_nBilateralFilterValue, g_nBilateralFilterValue*2, g_nBilateralFilterValue/2 );
	imshow("【<5>双边滤波】", g_dstImage5);
}

//-----------------------------------【ShowHelpText( )函数】-----------------------------
//		 描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
void ShowHelpText()
{
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第37个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");
}
```

&emsp;&emsp; (ii) Show results

![Image nonlinear filtering experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment1.png)

![Image nonlinear filtering experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment2.png)

![Image nonlinear filtering experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment3.png)

![Image nonlinear filtering experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment4.png)

![Image nonlinear filtering experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment5.png)

![Image nonlinear filtering experiment 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment6.png)

![Image nonlinear filtering experiment 7](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment7.png)

![Image nonlinear filtering experiment 8](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2004%20Image%20nonlinear%20filtering%20experiment/image-nonlinear-filtering-experiment8.png)

### Experiment summary

&emsp;&emsp;The main content of this experiment is to master the principle of median filtering and programming implementation method of image, and master the principle of bilateral filtering and programming implementation method of image. I used the medianBlur function in OpenCV to implement median filtering, and the bilateralFilter function in OpenCV to implement bilateral filtering. By writing code, I learned to implement median filtering and bilateral filtering using medianBlur and bilateralFilter functions.
