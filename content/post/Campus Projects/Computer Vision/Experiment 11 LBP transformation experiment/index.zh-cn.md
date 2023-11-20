---
title: 计算机视觉 - 实验十一 LBP变换实验
description: Computer Vision - Experiment 11 - LBP transformation experiment
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## 计算机视觉 - 实验十一 LBP变换实验

### 实验目的和要求

&emsp;&emsp;理解局部二值模式的基本原理；掌握实现局部二值模式的代码编写方法。

### 实验内容

&emsp;&emsp;（一）新建工程;

&emsp;&emsp;（二）在VS2015中配置OpenCV;

&emsp;&emsp;（三）读入原始图像并转换为灰度图像；

&emsp;&emsp;（四）实现LBP算法，计算输入图像的LBP纹理特征；

&emsp;&emsp;（五）显示LBP纹理特征图。

### 实验仪器、设备

&emsp;&emsp;计算机一台，已安装 Windows7操作系统和Visual Studio 2015

### 实验原理

&emsp;&emsp;（一）LBP指局部二值模式，英文全称:Local Binary Patterns。最初功能为辅助图像局部对比度，并不是一个完整的特征描述子。后来提升为一种有效的纹理描述算子，度量和提取图像局部的纹理信息，对光照具有不变性。LBP有很多变种，或说改进。单纯的LBP记录像素点与其周围像素点的对比信息，或说差异。

&emsp;&emsp;（二）LBP的基本思想是以图像中某个像素为中心，对相邻像素进行阈值比较。如果中心像素的亮度大于等于它的相邻像素，把相邻像素标记为0，否则标记为1。我们可以用二进制数字来表示LBP图中的每个像素的LBP编码。

### 实验步骤

&emsp;&emsp;（一）创建Visual Studio 2015控制台程序；

&emsp;&emsp;（二）在Visual Studio 2015中配置OpenCV；

&emsp;&emsp;（三）使用OpenCV的cvtColor函数将原始图像转换为灰度图像；

&emsp;&emsp;（四）编写函数，实现LBP算法，计算输入图像的LBP纹理特征；

&emsp;&emsp;（五）使用OpenCV的imshow函数显示LBP纹理特征图。

### 实验注意事项

&emsp;&emsp;（一）完成OpenCV安装之后，VS中配置OpenCV的方法；

&emsp;&emsp;（二）cvtColor函数的功能和使用方法；

&emsp;&emsp;（三）根据LBP算法的原理，用代码实现LBP算法。

### 实验结果

&emsp;&emsp;（一）实验代码

```cpp
#include <opencv2/opencv.hpp>
#include <limits>
using namespace std;
using namespace cv;

//原始的LBP算法
//使用模板参数
/**
*将原图去除最外围的一圈，里面的每个都作为中心点，来计算这个中心点相应矩形区域
*的lbp特征值。
*算出来的这个lbp特征值，就是目标mat的值，
*目标mat的大小是原始mat的（rows-2,cols-2)
*/
template <typename _Tp>
void OLBP_(const Mat& src, Mat& dst) {
	dst = Mat::zeros(src.rows - 2, src.cols - 2, CV_8UC1);
	for (int i = 1; i<src.rows - 1; i++) {
		for (int j = 1; j<src.cols - 1; j++) {
			_Tp center = src.at<_Tp>(i, j);
			unsigned char code = 0;
			code |= (src.at<_Tp>(i - 1, j - 1) > center) << 7;
			code |= (src.at<_Tp>(i - 1, j) > center) << 6;
			code |= (src.at<_Tp>(i - 1, j + 1) > center) << 5;
			code |= (src.at<_Tp>(i, j + 1) > center) << 4;
			code |= (src.at<_Tp>(i + 1, j + 1) > center) << 3;
			code |= (src.at<_Tp>(i + 1, j) > center) << 2;
			code |= (src.at<_Tp>(i + 1, j - 1) > center) << 1;
			code |= (src.at<_Tp>(i, j - 1) > center) << 0;
			dst.at<unsigned char>(i - 1, j - 1) = code;
			if (i == 1)
				cout << "(" << i - 1 << "," << j - 1 << ")=" << (unsigned)code << " ";
		}
		if (i == 1)
			cout << endl;
	}
}

template <typename _Tp>
void ELBP_(const Mat& src, Mat& dst, int radius, int neighbors) {
	neighbors = max(min(neighbors, 31), 1); // set bounds...
											// Note: alternatively you can switch to the new OpenCV Mat_
											// type system to define an unsigned int matrix... I am probably
											// mistaken here, but I didn't see an unsigned int representation
											// in OpenCV's classic typesystem...
	dst = Mat::zeros(src.rows - 2 * radius, src.cols - 2 * radius, CV_32SC1);
	for (int n = 0; n<neighbors; n++) {
		// sample points
		float x = static_cast<float>(radius) * cos(2.0*M_PI*n / static_cast<float>(neighbors));
		float y = static_cast<float>(radius) * -sin(2.0*M_PI*n / static_cast<float>(neighbors));
		// relative indices
		int fx = static_cast<int>(floor(x));
		int fy = static_cast<int>(floor(y));
		int cx = static_cast<int>(ceil(x));
		int cy = static_cast<int>(ceil(y));
		// fractional part
		float ty = y - fy;
		float tx = x - fx;
		// set interpolation weights
		float w1 = (1 - tx) * (1 - ty);
		float w2 = tx  * (1 - ty);
		float w3 = (1 - tx) *      ty;
		float w4 = tx  *      ty;
		// iterate through your data
		for (int i = radius; i < src.rows - radius; i++) {
			for (int j = radius; j < src.cols - radius; j++) {
				float t = w1*src.at<_Tp>(i + fy, j + fx) + w2*src.at<_Tp>(i + fy, j + cx) + w3*src.at<_Tp>(i + cy, j + fx) + w4*src.at<_Tp>(i + cy, j + cx);
				// we are dealing with floating point precision, so add some little tolerance
				dst.at<unsigned int>(i - radius, j - radius) += ((t > src.at<_Tp>(i, j)) && (abs(t - src.at<_Tp>(i, j)) > std::numeric_limits<float>::epsilon())) << n;
			}
		}
	}
}

int main(int argc, char* argv[]) {

	Mat color_face = imread("2007_000807.jpg", CV_LOAD_IMAGE_ANYDEPTH | CV_LOAD_IMAGE_ANYCOLOR);
	if (color_face.empty()) {
		cout << "read picture fail!\n";
		return -1;
	}

	Mat olbp_face = Mat::zeros(color_face.size(), color_face.type());

	//change to grey color picture
	cvtColor(color_face, olbp_face, CV_BGR2GRAY);

	//显示原始的输入图像
	cvNamedWindow("Src Image", CV_WINDOW_AUTOSIZE);
	imshow("Src Image", olbp_face);

	//计算输入图像的LBP纹理特征
	Mat lbp_face;//= Mat::zeros(color_face.size(),color_face.type()) ;
	OLBP_<uchar>(olbp_face, lbp_face);

	//显示LBP纹理特征图
	namedWindow("LBP Image1", 1);
	imshow("LBP Image1", lbp_face);


	//use elbp
	//  Mat elbp_face;
	//  ELBP_<uchar>(olbp_face,elbp_face,2,4);


	waitKey();

	return 0;
}
```

&emsp;&emsp;（二）显示结果

![LBP transformation experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment1.png)

![LBP transformation experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment2.png)

![LBP transformation experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment3.png)

![LBP transformation experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment4.png)

### 实验总结

&emsp;&emsp;本次实验的主要内容是理解局部二值模式的基本原理；掌握实现局部二值模式的代码编写方法。新建工程，在VS2015中配置OpenCV，读入原始图像并转换为灰度图像；实现LBP算法，计算输入图像的LBP纹理特征；显示LBP纹理特征图。学会了cvtColor函数的功能和使用方法；根据LBP算法的原理，用代码实现LBP算法。