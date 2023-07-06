---
title: Computer Vision - Experiment 16 - Separate background experiments with Gaussian background modeling
description: 计算机视觉 - 实验十六 用高斯背景建模分离背景实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验十六 用高斯背景建模分离背景实验

### 实验目的和要求

&emsp;&emsp;理解背景建模的基本原理；掌握实现背景建模的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用VideoCapture类打开视频；

&emsp;&emsp;（四）创建高斯混合模型；

&emsp;&emsp;（五）通过更新打开的视频的每一帧图像，对高斯混合模型进行更新;

&emsp;&emsp;（六）展示前景图像和背景图像。  

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio2015。

### 实验原理

&emsp;&emsp;（一）在很多情况下，我们需要从一段视频或者一系列图片中找到感兴趣的目标，比如说当人进入已经打烊的超市时发出警报。为了达到这个目的，我们首先需要“学习”背景模型，然后将背景模型和当前图像进行比较，从而得到前景目标。

&emsp;&emsp;（二）背景与前景都是相对的概念，以高速公路为例：有时我们对高速公路上来来往往的汽车感兴趣，这时汽车是前景，而路面以及周围的环境是背景；有时我们仅仅对闯入高速公路的行人感兴趣，这时闯入者是前景，而包括汽车之类的其他东西又成了背景。各种背景模型都有自己适用的场合。

&emsp;&emsp;（三）高斯混合模型(MOG)是OpenCv实现的一种高级的背景统计模型。高斯模型就是用高斯概率密度函数(正态分布曲线)精确地量化事物，将一个事物分解为若干的基于高斯概率密度函数(正态分布曲线)形成的模型。 对图像背景建立高斯模型的原理及过程:图像灰度直方图反映的是图像中某个灰度值出现的频次，也可以以为是图像灰度概率密度的估计。如果图像所包含的目标区域和背景区域相差比较大，且背景区域和目标区域在灰度上有一定的差异，那么该图像的灰度直方图呈现双峰-谷形状，其中一个峰对应于目标，另一个峰对应于背景的中心灰度。对于复杂的图像，尤其是医学图像，一般是多峰的。通过将直方图的多峰特性看作是多个高斯分布的叠加，可以解决图像的分割问题。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）调用VideoCapture的open函数打开视频；

&emsp;&emsp;（四）调用BackgroundSubtractorMOG2类创建高斯混合模型；

&emsp;&emsp;（五）调用VideoCapture类的“>>”方法读取视频中的一帧图像；

&emsp;&emsp;（六）通过更新打开的视频的每一帧图像，对高斯混合模型进行更新，调用getBackgroundImage函数获取背景图像;

&emsp;&emsp;（七）调用imshow函数展示前景图像和背景图像。 

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）VideoCapture类的功能和使用方法；

&emsp;&emsp;（三）BackgroundSubtractorMOG2类的功能和使用方法；

&emsp;&emsp;（四）getBackgroundImage函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//----------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/core/core.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include "opencv2/video/background_segm.hpp"
#include "opencv2/highgui/highgui.hpp"
#include <stdio.h>
using namespace std;
using namespace cv;


//-------------------------【help( )函数】--------------------------------------
//		 描述：输出一些帮助信息
//----------------------------------------------------------------------------------
static void help()
{
	printf("\n\n\n\t此程序展示了用高斯背景建模进行视频的背景分离方法.\n\n\t主要采用cvUpdateBGStatModel()函数\n"
		"\n\t程序首先会“学习背景”，然后进行分割。\n"
		"\n\t可以用过【Space】空格进行功能切换。\n\n");
}


//---------------------------【main( )函数】--------------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main(int argc, const char** argv)
{
	help();

	VideoCapture cap;
	bool update_bg_model = true;

	cap.open("1.avi");
	if( !cap.isOpened() )
	{
		printf("can not open camera or video file\n");
		return -1;
	}

	namedWindow("image", WINDOW_AUTOSIZE);
	namedWindow("foreground mask", WINDOW_AUTOSIZE);
	namedWindow("foreground image", WINDOW_AUTOSIZE);
	namedWindow("mean background image", WINDOW_AUTOSIZE);

	BackgroundSubtractorMOG2 bg_model;//(100, 3, 0.3, 5);

	Mat img, fgmask, fgimg;

	for(;;)
	{
		cap >> img;

		if( img.empty() )
			break;

		//cvtColor(_img, img, COLOR_BGR2GRAY);

		if( fgimg.empty() )
			fgimg.create(img.size(), img.type());

		//更新模型
		bg_model(img, fgmask, update_bg_model ? -1 : 0);

		fgimg = Scalar::all(0);
		img.copyTo(fgimg, fgmask);

		Mat bgimg;
		bg_model.getBackgroundImage(bgimg);

		imshow("image", img);
		imshow("foreground mask", fgmask);
		imshow("foreground image", fgimg);
		if(!bgimg.empty())
			imshow("mean background image", bgimg );

		char k = (char)waitKey(30);
		if( k == 27 ) break;
		if( k == ' ' )
		{
			update_bg_model = !update_bg_model;
			if(update_bg_model)
				printf("\t>背景更新(Background update)已打开\n");
			else
				printf("\t>背景更新(Background update)已关闭\n");
		}
	}

	return 0;
}
```

&emsp;&emsp;（二）显示结果

![Separate background experiments with Gaussian background modeling 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling1.png)

![Separate background experiments with Gaussian background modeling 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling2.png)

![Separate background experiments with Gaussian background modeling 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling3.png)

![Separate background experiments with Gaussian background modeling 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling4.png)

![Separate background experiments with Gaussian background modeling 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling5.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解背景建模的基本原理；掌握实现背景建模的代码编写方法。新建工程；在VS2015中配置OpenCV；使用VideoCapture类打开视频；创建高斯混合模型；通过更新打开的视频的每一帧图像，对高斯混合模型进行更新；展示前景图像和背景图像。