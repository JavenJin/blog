---
title: Computer Vision - Experiment 15 - Fast corner point detection experiments on video
description: 计算机视觉 - 实验十五 对视频的快速角点检测实验
date: '2020-06-10'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 15 - Fast corner point detection experiments on video

### Experimental objectives and requirements

&emsp;&emsp;Understand the basic principle of corner point detection; master the code writing method to implement corner point detection.

### Experiment content

&emsp;&emsp; (i) New project .

&emsp;&emsp; (ii) Configure OpenCV in VS2015.

&emsp;&emsp; (iii) Opening video files using the VideoCapture class;

&emsp;&emsp; (iv) Reading a frame from a video;

&emsp;&emsp; (v) Convert the grayscale map and detect the corner points.

&emsp;&emsp; (vi) traverse each point, plot it, and display the corner points in the original image.

### Experimental apparatus, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed.

### Experimental principle

&emsp;&emsp; (i) Corner point detection is a - method used in computer vision systems to obtain image features. A corner point is usually defined as the intersection of two edges, and more strictly speaking, the local neighborhood of a corner point should have two different regions with different directions of the boundary. In practice, most of the so-called corner detection methods detect image points with specific features, not just "corner points". These feature points have specific coordinates in the image and have certain mathematical characteristics, such as local maximum or minimum grayscale;

&emsp;&emsp; (ii) Corner points are used extensively to solve a range of problems such as object recognition, image recognition, image matching, visual tracking, and 3D reconstruction. Instead of looking at the whole picture, we select certain special points and then analyze them locally and purposefully. This method is of practical value if a sufficient number of such points can be detected, while they are well differentiated and stable features can be pinpointed;

&emsp;&emsp; (iii) A very important evaluation criterion for corner point detection methods is their ability to detect the same or similar features in multiple images and to cope with image changes such as lighting changes, image rotation, etc. The Shi-Tomasi algorithm is an improvement of the Harris algorithm,This experiment shows that for the same target in a video by playing a video, the Shi- Tomasi algorithm has a strong robustness for the corner points obtained for the same target in the video.

### Experimental steps

&emsp;&emsp; (i) Create a Visual Studio 2015 console program;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Call the open function of the VideoCapture class to open the video;

&emsp;&emsp; (iv) Call the ">>" method of the VideoCapture class to read a frame of the video;

&emsp;&emsp; (v) call the cvtColor function to convert the grayscale map and call the goodFeaturesToTrack function to detect the corner points.

&emsp;&emsp; (vi) traverse each point and call circle to plot the corner points in the original image.

### Experimental notes

&emsp;&emsp; (i) The method of configuring OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of the VideoCapture class;

&emsp;&emsp; (iii) The functions and usage of the cvtColor function;

&emsp;&emsp; (iv) The functions and usage of the goodFeaturesToTrack function.

### Experimental results

&emsp;&emsp; (i) Experimental code

```cpp
//------------------------------【头文件、命名空间包含部分】----------------------------
//		描述：包含程序所使用的头文件和命名空间
//-------------------------------------------------------------------------------------
#include "opencv2/calib3d/calib3d.hpp"
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/imgproc/imgproc.hpp"
#include "opencv2/features2d/features2d.hpp"
#include <iostream>
#include <list>
#include <vector>
using namespace std;
using namespace cv;
//---------------------------------【help( )函数】--------------------------------------
//		 描述：输出一些帮助信息
//-----------------------------------------------------------------------------------

int Harris(Mat &img)
{
	Mat grayImage;
	//转换灰度图
	cvtColor(img, grayImage, CV_BGR2GRAY);

	//开始进行角点检测  
	vector<Point2f> dstPoint2f;
	goodFeaturesToTrack(grayImage, dstPoint2f, 200, 0.01, 10, Mat(), 3);

	//遍历每个点，进行绘制，便于显示  
	//Mat dstImage;
	//img.copyTo(dstImage);
	for (int i = 0; i < (int)dstPoint2f.size(); i++)
	{
		circle(img, dstPoint2f[i], 3, Scalar(0,0,255), 2, 8);
	}
	return 0;
}
//---------------------------【main( )函数】--------------------------------------------
//		描述：控制台应用程序的入口函数，我们的程序从这里开始
//-------------------------------------------------------------------------------------
int main()
{
	VideoCapture capture;
	capture.open("1.avi");
	if (!capture.isOpened())
	{
		cout << "capture device " << " failed to open!" << endl;
		return 1;
	}
	Mat frame;
	Mat gray;
	for (;;)
	{
		capture >> frame;
		if (frame.empty())
			break;
		
		int h = frame.rows;
		int w = frame.cols;
		Harris(frame);
		imshow("frame", frame);
		waitKey(3);  //延时30ms
	}
	return 0;
} 
```

&emsp;&emsp; (ii) Show results

![Fast corner point detection experiments on video 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video1.png)

![Fast corner point detection experiments on video 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video2.png)

![Fast corner point detection experiments on video 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video3.png)

![Fast corner point detection experiments on video 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video4.png)

![Fast corner point detection experiments on video 5](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2015%20Fast%20corner%20point%20detection%20experiments%20on%20video/fast-corner-point-detection-experiments-on-video5.png)

### Experiment summary

&emsp;&emsp;The main content of this experiment is to understand the basic principle of corner point detection; master the code writing method to implement corner point detection. Create a new project; configure OpenCV in VS2015; open a video file using the VideoCapture class; read a frame from the video; convert the grayscale map and detect the corner points; traverse each point, draw, and display the corner points in the original map.