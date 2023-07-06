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

## Computer Vision - Experiment 10 - Create a rectangular boundary that encloses the outline

### Experimental objectives and requirements

&emsp;&emsp;Understand the basic principle of creating a rectangular boundary that encloses an outline; master the method of writing code to create a rectangular boundary that encloses an outline using OpenCV.

### Experiment content

&emsp;&emsp; (i) Create a new project.

&emsp;&emsp; (ii) Configuring OpenCV in VS2015.

&emsp;&emsp; (iii) Randomly generate point coordinates using the RNG class in OpenCV;

&emsp;&emsp; (iv) Finding the enclosing rectangle of minimum area for a given set of 2D points;

&emsp;&emsp; (v) Draw the enclosing rectangle with the minimum area.

### Experimental apparatus, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed

### Experimental principle

&emsp;&emsp; (i) In practical applications, there is often a need to represent the detected contour as a polygon. This experiment implements how to represent the outline with a rectangle, or how to extract the rectangle based on the outline.

&emsp;&emsp; (ii) In OpenCV, using the RNG class, you can randomly generate point coordinates and then use the minAreaRect function to find the enclosing rectangle with the smallest area. The rectangle obtained by the minAreaRect function can have a deflection angle and can be parallel to the
the boundaries of the image are not parallel.

### Experimental steps

&emsp;&emsp; (i) Create a Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Write code to randomly generate point coordinates using the RNG class in OpenCV;

&emsp;&emsp; (iv) Write code to find the minimum area enclosing rectangle for the 2D point set generated in the previous step, using the minAreaRect function in OpenCV;

&emsp;&emsp; (v) Write code to draw the enclosing rectangle with the smallest area detected by the minAreaRect function, using the line function in OpenCV.

### Experimental notes

&emsp;&emsp; (i) Configure OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of the RNG class;

&emsp;&emsp; (iii) The functions and usage of the minAreaRect function;

&emsp;&emsp; (iv) The functions and usage of the line function.

### Experimental results

&emsp;&emsp; (i) Experimental code

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

&emsp;&emsp; (ii) Show the results

![Create a rectangular boundary that encloses the outline 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline1.png)

![Create a rectangular boundary that encloses the outline 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline2.png)

![Create a rectangular boundary that encloses the outline 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline3.png)

![Create a rectangular boundary that encloses the outline 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2010%20Create%20a%20rectangular%20boundary%20that%20encloses%20the%20outline/create-a-rectangular-boundary-that-encloses-the-outline4.png)

### Experiment Summary

&emsp;&emsp;The main content of this experiment is to understand the basic principle of creating a rectangular boundary that encloses an outline; to master the code writing method of creating a rectangular boundary that encloses an outline using OpenCV. Create a new project, configure OpenCV in VS2015, use the RNG class in OpenCV to randomly generate point coordinates; find the enclosing rectangle with the minimum area for a given set of 2D points; draw the enclosing rectangle with the minimum area. Learned to randomly generate point coordinates using the RNG class in OpenCV; learned how to find the enclosing rectangle with the smallest area for a given set of 2D points; learned how to draw the enclosing rectangle with the smallest area.