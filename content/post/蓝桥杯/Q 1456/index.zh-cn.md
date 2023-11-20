---
title: 题目 1456 [历届试题]连号区间数 (C语言)
description: Q 1456 [Past Test Questions]Number of consecutive number intervals (C Language)
date: '2019-04-01'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1456: \[历届试题\]连号区间数
时间限制: 1Sec 内存限制: 128MB
## 题目描述
小明这些天一直在思考这样一个奇怪而有趣的问题：
在1~N的某个全排列中有多少个连号区间呢？这里所说的连号区间的定义是：
如果区间[L,  R]  里的所有元素（即此排列的第L个到第R个元素）递增排序后能得到一个长度为R-L+1的“连续”数列，则称这个区间连号区间。
当N很小的时候，小明可以很快地算出答案，但是当N变大的时候，问题就不是那么简单了，现在小明需要你的帮助。
## 输入
第一行是一个正整数N  (1  < =  N  < =  50000),  表示全排列的规模。 
第二行是N个不同的数字Pi(1  < =  Pi  < =  N)，  表示这N个数字的某一全排列。
## 输出
输出一个整数，表示不同连号区间的数目。
## 样例输入
```
5
3 4 2 5 1
```
## 样例输出
```
9
```
## C代码
```c
#include<stdio.h>
int main()
{
	long int n,i,j,max,min,sum=0;
	scanf("%ld",&n);
	long int a[n+1];    
	for(i=1;i<=n;i++)
		scanf("%ld",&a[i]);
	for(i=1;i<n;i++)//表示 从第i位开始的区间 
	{
		min=max=a[i];
		for(j=i+1;j<=n;j++)//表示到结束在j位
		{    
    		if(a[j]<min){min=a[j];}
    		if(a[j]>max){max=a[j];}
			if(max-min==j-i) sum++; 
			//如果区间最大值与最小值之差等于当前区间数 j-i 则此区间必然重排后必然连续 
		}
	}
	printf("%ld\n",sum+n);
	return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行