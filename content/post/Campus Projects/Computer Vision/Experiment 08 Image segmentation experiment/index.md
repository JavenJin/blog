---
title: Computer Vision - Experiment 8 - Image segmentation experiment
description: 计算机视觉 - 实验八 图像分割实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 8 - Image segmentation experiment

### Experimental objectives and requirements

&emsp;&emsp;Understand the basic principle of image segmentation using meanShfit; master the code writing method of color image segmentation by mean drift algorithm using OpenCV.

### Experiment content

&emsp;&emsp; (i) Create a new project.

&emsp;&emsp; (ii) Configuring OpenCV in VS2015.

&emsp;&emsp; (iii) Implementing color image segmentation using pyrMeanShiftFiltering function in OpenCV;

&emsp;&emsp; (iv) Use the floodFill function in OpenCV to fill the result of its segmentation with different colors.

### Experimental apparatus, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed

### Experimental principle

&emsp;&emsp; (i) meanShfit (mean drift) algorithm is a general clustering algorithm, its basic principle is: for a given number of samples, any one of the samples, the sample as the center point to delineate a circular region, find the center of mass of the samples in the circular region, that is, the point at the maximum density, and then continue to perform the above iterative process with that point as the center until the final convergence.

&emsp;&emsp; (ii) meanShfit can be used not only for image filtering, video tracking, but also for image segmentation. The corresponding function in Opencv is pyrMeanShiftFiltering. pyrMeanShiftFiltering is an image smoothing filter at the color level, which can neutralize colors with similar color distribution, smooth out color details, and erode smaller color areas, thus achieve the segmentation effect.

&emsp;&emsp; (iii) The main process of this experiment is to first set up the parameters and then use the function pyrMeanShiftFiltering function to segment the input image. The result of the segmentation is saved in the second parameter of the function that is the output image, and finally the result of its segmentation is filled with different colors according to the characteristics of this segmented image using the floodFill function.

### Experimental steps

&emsp;&emsp; (i) Create the Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Write code to implement color image segmentation using pyrMeanShiftFiltering function;

&emsp;&emsp; (iv) Write code to fill the result of its segmentation with different colors using the floodFill function.

### Experimental notes

&emsp;&emsp; (i) Configure OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of pyrMeanShiftFiltering function;

&emsp;&emsp; (iii) The functions and usage of the floodFill function.

### Experimental results

&emsp;&emsp; (i) Experimental code

```cpp
//-------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/core/core.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include <iostream>
using namespace cv;
using namespace std;


//---------------------------------【help( )函数】--------------------------------------
//		 描述：输出一些帮助信息
//-------------------------------------------------------------------------------------
static void help()
{
	cout << "\n\t此程序演示了OpenCV中MeanShift图像分割的使用。\n"
		<< "\n\t程序运行后我们可以通过3个滑动条调节分割效果。调节滑动条后可能会有些许卡顿，请耐心等待\n"
		<< "\n\t3个滑动条代表的参数分别为空间窗的半径 （spatialRad）、色彩窗的半径（colorRad）、最大图像金字塔级别（maxPyrLevel）\n"
		<< endl;
}


//This colors the segmentations
static void floodFillPostprocess( Mat& img, const Scalar& colorDiff=Scalar::all(1) )
{
	CV_Assert( !img.empty() );
	RNG rng = theRNG();
	Mat mask( img.rows+2, img.cols+2, CV_8UC1, Scalar::all(0) );
	for( int y = 0; y < img.rows; y++ )
	{
		for( int x = 0; x < img.cols; x++ )
		{
			if( mask.at<uchar>(y+1, x+1) == 0 )
			{
				Scalar newVal( rng(256), rng(256), rng(256) );
				floodFill( img, mask, Point(x,y), newVal, 0, colorDiff, colorDiff );
			}
		}
	}
}

string winName = "meanshift";
int spatialRad, colorRad, maxPyrLevel;
Mat img, res;



static void meanShiftSegmentation( int, void* )
{
	cout << "spatialRad=" << spatialRad << "; "
		<< "colorRad=" << colorRad << "; "
		<< "maxPyrLevel=" << maxPyrLevel << endl;
	pyrMeanShiftFiltering( img, res, spatialRad, colorRad, maxPyrLevel );
	floodFillPostprocess( res, Scalar::all(2) );
	imshow( winName, res );
}



//--------------------------【main( )函数】--------------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//------------------------------------------------------------------------------------
int main(int argc, char** argv)
{

	help();

	img = imread( "1.jpg" );
	if( img.empty() )
		return -1;
	imshow("原始图",img);
	spatialRad = 10;
	colorRad = 10;
	maxPyrLevel = 1;

	namedWindow( winName, WINDOW_AUTOSIZE );

	createTrackbar( "spatialRad", winName, &spatialRad, 80, meanShiftSegmentation );
	createTrackbar( "colorRad", winName, &colorRad, 60, meanShiftSegmentation );
	createTrackbar( "maxPyrLevel", winName, &maxPyrLevel, 5, meanShiftSegmentation );

	meanShiftSegmentation(0, 0);
	waitKey();
	return 0;
}
```

&emsp;&emsp; (ii) Show results

![Image segmentation experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet1.png)

![Image segmentation experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet2.png)

![Image segmentation experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet3.png)

![Image segmentation experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet4.png)

![Image segmentation experiment 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2008%20Image%20segmentation%20experiment/image-segmentation-experimet5.png)

### Experiment Summary

&emsp;&emsp;The main content of this experiment is to understand the basic principle of image segmentation using meanShfit; to master the code writing method of color image segmentation by meanShift algorithm using OpenCV. Create a new project, configure OpenCV in VS2015, use pyrMeanShiftFiltering function in OpenCV to achieve color image segmentation; use the floodFill function in OpenCV to fill the result of its segmentation with different colors. Learn to implement color image segmentation using pyrMeanShiftFiltering function; floodFill function to fill the result of its segmentation with different colors.