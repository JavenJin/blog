---
title: Computer Vision - Experiment 16 - Separate background experiments with Gaussian background modeling
description: 计算机视觉 - 实验十六 用高斯背景建模分离背景实验
date: '2020-06-12'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 16 - Separate background experiments with Gaussian background modeling

### Experimental objectives and requirements

&emsp;&emsp;Understand the basic principles of background modeling; master the code writing method to implement background modeling.

### Experiment content

&emsp;&emsp; (i) Create a new project.

&emsp;&emsp; (ii) Configure OpenCV in VS2015.

&emsp;&emsp; (iii) Opening a video using the VideoCapture class;

&emsp;&emsp; (iv) Creating a Gaussian blend model;

&emsp;&emsp; (v) Update the Gaussian blending model by updating each image frame of the opened video.

&emsp;&emsp; (vi) Show the foreground image and the background image.  

### Experimental apparatus, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed.

### Experimental principle

&emsp;&emsp; (i) In many cases, we need to find the target of interest from a video or a series of images, for example, to sound an alarm when a person enters a supermarket that is already closed. To do this, we first need to "learn" the background model, and then compare the background model with the current image to get the foreground target.

&emsp;&emsp; (ii) background and foreground are relative concepts, take the highway as an example: sometimes we are interested in the cars coming and going on the highway, then the cars are the foreground, while the road and the surrounding environment are the background; sometimes we are only interested in the pedestrians breaking into the highway, then the intruders are the foreground, while other things, including cars, become the background. All kinds of background models have their own application occasions.

&emsp;&emsp; (iii) Mixture of Gaussians (MOG) is an advanced background statistical model implemented by OpenCv. Gaussian model is to quantify things precisely with Gaussian probability density function (normal distribution curve), and decompose one thing into several models formed based on Gaussian probability density function (normal distribution curve). The principle and process of building a Gaussian model for an image background:The image gray histogram reflects the frequency of occurrence of a certain gray value in an image, which can also be thought of as an estimate of the image gray probability density. If the target area and the background area contained in the image are relatively different, and the background area and the target area have a certain difference in gray level, then the gray level histogram of the image shows a double peak-valley shape, where one peak corresponds to the target and the other peak corresponds to the central gray level of the background. For complex images, especially medical images, they are usually multi-peaked. By considering the multi-peak property of the histogram as a superposition of multiple Gaussian distributions, the image segmentation problem can be solved.

### Experimental steps

&emsp;&emsp; (i) Create a Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Call the open function of VideoCapture to open the video;

&emsp;&emsp; (iv) Calling the BackgroundSubtractorMOG2 class to create a Gaussian mixture model;

&emsp;&emsp; (v) Call the ">>" method of the VideoCapture class to read a frame of the video;

&emsp;&emsp; (vi) Update the Gaussian blending model by updating each frame of the opened video and calling the getBackgroundImage function to get the background image.

&emsp;&emsp; (vii) Call the imshow function to display the foreground image and the background image. 

### Experimental notes

&emsp;&emsp; (i) The method of configuring OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of the VideoCapture class;

&emsp;&emsp; (iii) The functions and usage of the BackgroundSubtractorMOG2 class;

&emsp;&emsp; (iv) The functions and usage of getBackgroundImage function.

### Experimental results

&emsp;&emsp; (i) Experimental code

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

&emsp;&emsp; (ii) Show results

![Separate background experiments with Gaussian background modeling 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling1.png)

![Separate background experiments with Gaussian background modeling 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling2.png)

![Separate background experiments with Gaussian background modeling 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling3.png)

![Separate background experiments with Gaussian background modeling 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling4.png)

![Separate background experiments with Gaussian background modeling 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2016%20Separate%20background%20experiments%20with%20Gaussian%20background%20modeling/separate-background-experiments-with-gaussian-background-modeling5.png)

### Experiment summary

&emsp;&emsp;The main content of this experiment is to understand the basic principles of background modeling; master the code writing method to implement background modeling. Create a new project; configure OpenCV in VS2015; open a video using the VideoCapture class; create a Gaussian blending model; update the Gaussian blending model by updating each frame of the opened video; display the foreground image and the background image.