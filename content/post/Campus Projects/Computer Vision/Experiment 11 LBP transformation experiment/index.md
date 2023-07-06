---
title: Computer Vision - Experiment 11 - LBP transformation experiment
description: 计算机视觉 - 实验十一 LBP变换实验
date: '2020-04-20'
categories:
    - Computer Vision
tags:
    - Computer Vision
    - OpenCV
---

## Computer Vision - Experiment 11 - LBP transformation experiment

### Experimental objectives and requirements

&emsp;&emsp;Understand the basic principle of local binary pattern; master the code writing method to implement local binary pattern.

### Experiment content

&emsp;&emsp; (i) Create a new project.

&emsp;&emsp; (ii) Configuring OpenCV in VS2015.

&emsp;&emsp; (iii) Read in the original image and convert it to grayscale;

&emsp;&emsp; (iv) Implement the LBP algorithm and calculate the LBP texture features of the input image;

&emsp;&emsp; (v) Display the LBP texture feature map.

### Experimental apparatus, equipment

&emsp;&emsp;A computer with Windows 7 operating system and Visual Studio 2015 installed

### Experimental principle

&emsp;&emsp; (i) LBP refers to Local Binary Patterns, full name in English:Local Binary Patterns. initially functioned as an aid to image local contrast, and was not a complete feature descriptor. LBP has many variants, or improvements. Simple LBP records information about the contrast, or difference, between a pixel point and its surrounding pixel points.

&emsp;&emsp; (ii) The basic idea of LBP is to compare the threshold value of neighboring pixels with a pixel in the image as the center. If the brightness of the center pixel is greater than or equal to its neighboring pixels, mark the neighboring pixel as 0, otherwise mark it as 1. We can use binary numbers to represent the LBP code of each pixel in the LBP graph.

### Experimental steps

&emsp;&emsp; (i) Create a Visual Studio 2015 console application;

&emsp;&emsp; (ii) Configure OpenCV in Visual Studio 2015;

&emsp;&emsp; (iii) Converting the original image to grayscale using OpenCV's cvtColor function;

&emsp;&emsp; (iv) Write functions to implement the LBP algorithm to calculate the LBP texture features of the input image;

&emsp;&emsp; (v) Use the imshow function of OpenCV to display the LBP texture feature map.

### Experimental Notes

&emsp;&emsp; (i) The method of configuring OpenCV in VS after completing the installation of OpenCV;

&emsp;&emsp; (ii) The functions and usage of the cvtColor function;

&emsp;&emsp; (iii) The implementation of LBP algorithm in code based on the principle of LBP algorithm.

### Experimental results

&emsp;&emsp; (i) Experimental code

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

&emsp;&emsp; (ii) Show results

![LBP transformation experiment 1](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment1.png)

![LBP transformation experiment 2](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment2.png)

![LBP transformation experiment 3](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment3.png)

![LBP transformation experiment 4](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Campus%20Projects/Computer%20Vision/Experiment%2011%20LBP%20transformation%20experiment/lbp-transformation-experiment4.png)

### Experiment summary

&emsp;&emsp;The main content of this experiment is to understand the basic principle of the local binary pattern; master the code writing method to implement the local binary pattern. Create a new project, configure OpenCV in VS2015, read in the original image and convert it to grayscale image; implement the LBP algorithm to calculate the LBP texture features of the input image; display the LBP texture feature map. Learned the functions and usage of cvtColor function; Implemented LBP algorithm in code according to the principle of LBP algorithm.