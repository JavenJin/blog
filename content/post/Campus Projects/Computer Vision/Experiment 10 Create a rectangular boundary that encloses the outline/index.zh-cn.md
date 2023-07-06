---
title: Computer Vision - Experiment 10 - Create a rectangular boundary that encloses the outline
description: 计算机视觉 - 实验十 创建包围轮廓的矩形边界
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验十 创建包围轮廓的矩形边界

### 实验目的和要求

&emsp;&emsp;理解创建包围轮廓的矩形边界的基本原理；掌握使用OpenCV创建包围轮廓的矩形边界的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）使用OpenCV中的RNG类随机生成点坐标；

&emsp;&emsp;（四）对给定的 2D 点集，寻找最小面积的包围矩形；

&emsp;&emsp;（五）绘制出最小面积的包围矩形。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）在实际应用中，常常会有将检测到的轮廓用多边形表示出来的需求。本实验实现如何用矩形来表示轮廓，或者说如何根据轮廓提取出矩形。

&emsp;&emsp;（二）在OpenCV中，使用RNG类可以随机生成点坐标，然后使用minAreaRect函数寻找最小面积的包围矩形，minAreaRect函数求得的矩形是可以有偏转角度的，可以与
图像的边界不平行。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）编写代码，使用OpenCV中的RNG类随机生成点坐标；

&emsp;&emsp;（四）编写代码，使用OpenCV中的minAreaRect函数，对上一步生成的2D点集，寻找最小面积的包围矩形；

&emsp;&emsp;（五）编写代码，使用OpenCV中的line函数，绘制出minAreaRect函数检测到的最小面积的包围矩形。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）RNG类的功能和使用方法；

&emsp;&emsp;（三）minAreaRect函数的功能和使用方法；

&emsp;&emsp;（四）line函数的功能和使用方法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
//---------------------------------【头文件、命名空间包含部分】--------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
using namespace cv;
using namespace std;


//-----------------------------------【ShowHelpText( )函数】-----------------------------
//          描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
static void ShowHelpText()
{

	//输出欢迎信息和OpenCV版本
	printf("\n\n\t\t\t非常感谢购买《OpenCV3编程入门》一书！\n");
	printf("\n\n\t\t\t此为本书OpenCV3版的第73个配套示例程序\n");
	printf("\n\n\t\t\t   当前使用的OpenCV版本为：" CV_VERSION );
	printf("\n\n  ----------------------------------------------------------------\n");

	//输出一些帮助信息
	printf("\n\n\n\t\t\t欢迎来到【矩形包围示例】示例程序~\n\n"); 
	printf("\n\n\t按键操作说明: \n\n" 
		"\t\t键盘按键【ESC】、【Q】、【q】- 退出程序\n\n" 
		"\t\t键盘按键任意键 - 重新生成随机点，并寻找最小面积的包围矩形\n" );  
}

int main(  )
{
	//改变console字体颜色
	system("color 1F"); 

	//显示帮助文字
	ShowHelpText();

	//初始化变量和随机值
	Mat image(600, 600, CV_8UC3);
	RNG& rng = theRNG();

	//循环，按下ESC,Q,q键程序退出，否则有键按下便一直更新
	while(1)
	{
		//参数初始化
		int count = rng.uniform(3, 103);//随机生成点的数量
		vector<Point> points;//点值

		//随机生成点坐标
		for(int  i = 0; i < count; i++ )
		{

			Point point;
			point.x = rng.uniform(image.cols/4, image.cols*3/4);
			point.y = rng.uniform(image.rows/4, image.rows*3/4);

			points.push_back(point);
		}

		//对给定的 2D 点集，寻找最小面积的包围矩形
		RotatedRect box = minAreaRect(Mat(points));
		Point2f vertex[4];
		box.points(vertex);

		//绘制出随机颜色的点
		image = Scalar::all(0);
		for( int i = 0; i < count; i++ )
			circle( image, points[i], 3, Scalar(rng.uniform(0, 255), rng.uniform(0, 255), rng.uniform(0, 255)), FILLED, LINE_AA );


		//绘制出最小面积的包围矩形
		for( int i = 0; i < 4; i++ )
			line(image, vertex[i], vertex[(i+1)%4], Scalar(100, 200, 211), 2, LINE_AA);

		//显示窗口
		imshow( "矩形包围示例", image );

		//按下ESC,Q,或者q，程序退出
		char key = (char)waitKey();
		if( key == 27 || key == 'q' || key == 'Q' ) // 'ESC'
			break;
	}

	return 0;
}
```

&emsp;&emsp;（二）显示结果

![Create a rectangular boundary that encloses the outline 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline1.png)

![Create a rectangular boundary that encloses the outline 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline2.png)

![Create a rectangular boundary that encloses the outline 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline3.png)

![Create a rectangular boundary that encloses the outline 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline4.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解创建包围轮廓的矩形边界的基本原理；掌握使用OpenCV创建包围轮廓的矩形边界的代码编写方法。新建工程，在VS2015中配置OpenCV，使用OpenCV中的RNG类随机生成点坐标；对给定的 2D 点集，寻找最小面积的包围矩形；绘制出最小面积的包围矩形。学会了用OpenCV中的RNG类随机生成点坐标；学会了对给定的 2D 点集，如何寻找最小面积的包围矩形；学会了如何绘制出最小面积的包围矩形。