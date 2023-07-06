---
title: Computer Vision - Experiment 1 - Image loading, display and output
description: 计算机视觉 - 实验一 图像的载入、显示与输出
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 1 - Image loading, display and output

### Experimental objectives and requirements

&emsp;&emsp; (i) To master the installation of OpenCV in Windows through experiments;

&emsp;&emsp; (ii) master the method of loading, displaying and outputting images through experiments

### Experiment content

&emsp;&emsp; (i) Installing OpenCV in Windows.

&emsp;&emsp; (ii) Write programs for loading, displaying and outputting images.

### Experimental instruments, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed

### Experimental principle

&emsp;&emsp;Opencv uses the Mat class to implement image storage. Images are stored in a matrix format where each pixel has a position and can be referenced by the number of columns and rows. the Mat class is not only used to store images, but also different types of matrices of arbitrary size. The Mat class can be used to perform operations such as matrix addition, matrix multiplication, matrix creation, etc. The imread function is used to read the image. imwrite function is used to write the image. imshow function is used to display the image.

### Experimental steps

&emsp;&emsp; (i) Install OpenCV in Windows

&emsp;&emsp;Download opencv source code in the URL [https://sourceforge.net/projects/opencvlibrary/](https://sourceforge.net/projects/opencvlibrary/) and install it in Windows to install OpenCV.

&emsp;&emsp; (ii) Configuring OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Write code to read the image using the imread function;

&emsp;&emsp; (iv) Write code to write images using the imwrite function;

&emsp;&emsp; (v) Write code to display the image using the imshow function.

### Experimental notes

&emsp;&emsp; (i) Configure OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of imread, imwrite, and imshow functions.

### Experimental results

&emsp;&emsp; (i) Experimental code

```cpp
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
using namespace cv;


int main( )
{
	//-------------------------------【一、图像的载入和显示】----------------------------
	//	描述：以下三行代码用于完成图像的载入和显示
	//---------------------------------------------------------------------------------
	
	cv::Mat girl = cv::imread("girl.jpg", 0); //载入图像到Mat
	namedWindow("【1】动漫图"); //创建一个名为 "【1】e动漫图"的窗口  
	imshow("【1】动漫图",girl);//显示名为 "【1】动漫图"的窗口  

	//-------------------------------【二、初级图像混合】---------------------------------
	//	描述：二、初级图像混合
	//---------------------------------------------------------------------------------
	//载入图片
	Mat image = imread("dota.jpg");
	Mat logo = imread("dota_logo.jpg");

	//载入后先显示
	namedWindow("【2】原画图");
	imshow("【2】原画图",image);

	namedWindow("【3】logo图");
	imshow("【3】logo图",logo);

	// 定义一个Mat类型，用于存放，图像的ROI
	Mat imageROI;
	//方法一
	imageROI= image(Rect(800,350,logo.cols,logo.rows));
	//方法二
	//imageROI= image(Range(350,350+logo.rows),Range(800,800+logo.cols));

	// 将logo加到原图上
	addWeighted(imageROI,0.5,logo,0.3,0.,imageROI);

	//显示结果
	namedWindow("【4】原画+logo图");
	imshow("【4】原画+logo图",image);

	//--------------------------------【三、图像的输出】----------------------------------
	//	描述：将一个Mat图像输出到图像文件
	//---------------------------------------------------------------------------------
	//输出一张jpg图片到工程目录下
	imwrite("由imwrite生成的图片.jpg", image);
	//imwrite("由imwrite生成的图片.jpg", image);

	waitKey(0);

	return 0;
}
```

&emsp;&emsp; (ii) Show results

![Image loading, display and output 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output1.jpeg)

![Image loading, display and output 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output2.jpeg)

![Image loading, display and output 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output3.jpeg)

![Image loading, display and output 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output4.jpeg)

![Image loading, display and output 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output5.jpeg)

![Image loading, display and output 6](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2001%20Image%20loading%2C%20display%20and%20output/image-loading-display-and-output6.jpeg)

### Experiment Summary

&emsp;&emsp;The main content of this experiment is to write a program for loading, displaying and outputting images. The main functions used are cv::Mat girl=cv::imread("xx.jpg", 0); (load image to Mat, the first parameter xx.jpg is the name of the image, the second parameter 0 is the grayscale map); namedWindow("window name");; display function imshow("window name", xx);; load image function Mat image= imread("xx.jpg");; imageROI= image(Rect());; addWeighted();; imwrite(".jpg",image);;; etc. functions. This experiment allowed me to fully understand the above functions and the flow of the experiment. I learned how to use the above functions to load, display and input the most basic images by myself.
