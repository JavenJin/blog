---
title: Computer Vision - Experiment 12 - Discrete Fourier Transform Experiment
description: 计算机视觉 - 实验十二 离散傅里叶变换实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验十二 离散傅里叶变换实验

### 实验目的和要求

&emsp;&emsp;理解傅立叶变换的基本原理；掌握实现傅立叶变换的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）以灰度模式读取原始图像并显示；

&emsp;&emsp;（四）编写代码实现傅立叶变换；

&emsp;&emsp;（五）显示傅立叶变换效果图。  

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）离散傅里叶变换(DFT)，是指傅里叶变换在时域和频域上都呈现离散的形式，将时域信号的采样变换为在离散时间傅里叶变换频域的采样。在形式上，变换两端（时域和频域上）的序列是有限长的，而实际上这两组序列都应当被认为是离散周期信号的主值序列。 即使对有限长的离散信号做DFT，也应当对其经过周期延拓成为周期信号再进行变换。在实际应用中，通常采用快速傅里叶变换来高效计算DFT。

&emsp;&emsp;（二）在频域里面，对于一幅图像，亮度或灰度变化激烈的地方对应高频成分，如边缘、纹理信息；亮度或灰度变化不大的地方对应低频成分。如果图像受到的噪声恰好位于某个特定的“频率”范围内，则可以通过滤波器来恢复原来的图像。傅里叶变换在图像处理中可以做到图像增强与图像去噪、图像分割之边缘检测、图像特征提取、图像压缩等。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）以灰度模式读取原始图像并显示；

&emsp;&emsp;（四）将输入图像延扩到最佳的尺寸，边界用0补充；

&emsp;&emsp;（五）为傅立叶变换的结果(实部和虚部)分配存储空间；

&emsp;&emsp;（六）进行离散傅里叶变换；

&emsp;&emsp;（七）将复数转换为幅值；

&emsp;&emsp;（八）进行对数尺度缩放；

&emsp;&emsp;（九）剪切和重分布幅度图象限；

&emsp;&emsp;（十）归一化，用0到1之间的浮点值将矩阵变换为可视的图像格式；

&emsp;&emsp;（十一）显示傅立叶变换效果图。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）dft函数的功能和使用方法；

&emsp;&emsp;（三）剪切和重分布幅度图象限的方法；

&emsp;&emsp;（四）normalize函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//-----------------------【头文件、命名空间包含部分】-----------------------------
//		描述：包含程序所使用的头文件和命名空间
//---------------------------------------------------------------------------------
#include "opencv2/core/core.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include "opencv2/highgui/highgui.hpp"
#include <iostream>
using namespace cv;


//-----------------------------------【ShowHelpText( )函数】------------------------
//		 描述：输出一些帮助信息
//----------------------------------------------------------------------------------
void ShowHelpText()
{
	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第28个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------------------\n");
}



//-------------------------------【main( )函数】-----------------------------------------
//          描述：控制台应用程序的入口函数，我们的程序从这里开始执行
//-------------------------------------------------------------------------------------
int main( )
{

	//【1】以灰度模式读取原始图像并显示
	Mat srcImage = imread("feng.png", 0);
	if(!srcImage.data ) { printf("读取图片错误，请确定目录下是否有imread函数指定图片存在~！ \n"); return false; } 
	imshow("原始图像" , srcImage);   

	ShowHelpText();

	//【2】将输入图像延扩到最佳的尺寸，边界用0补充
	int m = getOptimalDFTSize( srcImage.rows );
	int n = getOptimalDFTSize( srcImage.cols ); 
	//将添加的像素初始化为0.
	Mat padded;  
	copyMakeBorder(srcImage, padded, 0, m - srcImage.rows, 0, n - srcImage.cols, BORDER_CONSTANT, Scalar::all(0));

	//【3】为傅立叶变换的结果(实部和虚部)分配存储空间。
	//将planes数组组合合并成一个多通道的数组complexI
	Mat planes[] = {Mat_<float>(padded), Mat::zeros(padded.size(), CV_32F)};
	Mat complexI;
	merge(planes, 2, complexI);         

	//【4】进行就地离散傅里叶变换
	dft(complexI, complexI);           

	//【5】将复数转换为幅值，即=> log(1 + sqrt(Re(DFT(I))^2 + Im(DFT(I))^2))
	split(complexI, planes); // 将多通道数组complexI分离成几个单通道数组，planes[0] = Re(DFT(I), planes[1] = Im(DFT(I))
	//void magnitude(InputArray x, InputArray y, OutputArray magnitude);
	magnitude(planes[0], planes[1], planes[0]);// planes[0] = magnitude  
	Mat magnitudeImage = planes[0];

	//【6】进行对数尺度(logarithmic scale)缩放
	magnitudeImage += Scalar::all(1);
	log(magnitudeImage, magnitudeImage);//求自然对数

	//【7】剪切和重分布幅度图象限
	//若有奇数行或奇数列，进行频谱裁剪      
	magnitudeImage = magnitudeImage(Rect(0, 0, magnitudeImage.cols & -2, magnitudeImage.rows & -2));
	//重新排列傅立叶图像中的象限，使得原点位于图像中心  
	int cx = magnitudeImage.cols/2;
	int cy = magnitudeImage.rows/2;
	Mat q0(magnitudeImage, Rect(0, 0, cx, cy));   // ROI区域的左上
	Mat q1(magnitudeImage, Rect(cx, 0, cx, cy));  // ROI区域的右上
	Mat q2(magnitudeImage, Rect(0, cy, cx, cy));  // ROI区域的左下
	Mat q3(magnitudeImage, Rect(cx, cy, cx, cy)); // ROI区域的右下
	//交换象限（左上与右下进行交换）
	Mat tmp;                           
	q0.copyTo(tmp);
	q3.copyTo(q0);
	tmp.copyTo(q3);
	//交换象限（右上与左下进行交换）
	q1.copyTo(tmp);                 
	q2.copyTo(q1);
	tmp.copyTo(q2);

	//【8】归一化，用0到1之间的浮点值将矩阵变换为可视的图像格式
	//此句代码的OpenCV2版为：
	//normalize(magnitudeImage, magnitudeImage, 0, 1, CV_MINMAX); 
	//此句代码的OpenCV3版为:
	normalize(magnitudeImage, magnitudeImage, 0, 1, NORM_MINMAX); 

	//【9】显示效果图
	imshow("频谱幅值", magnitudeImage);    
	waitKey();

	return 0;
}
```

&emsp;&emsp;（二）显示结果

![Discrete Fourier Transform Experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2012%20Discrete%20Fourier%20Transform%20Experiment/discrete-fourier-transform-experiment1.png)

![Discrete Fourier Transform Experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2012%20Discrete%20Fourier%20Transform%20Experiment/discrete-fourier-transform-experiment2.png)

![Discrete Fourier Transform Experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2012%20Discrete%20Fourier%20Transform%20Experiment/discrete-fourier-transform-experiment3.png)

![Discrete Fourier Transform Experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2012%20Discrete%20Fourier%20Transform%20Experiment/discrete-fourier-transform-experiment4.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解傅立叶变换的基本原理；掌握实现傅立叶变换的代码编写方法。新建工程，在VS2015中配置OpenCV；以灰度模式读取原始图像并显示；编写代码实现傅立叶变换；显示傅立叶变换效果图。