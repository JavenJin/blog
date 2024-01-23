---
title: 题目 1432 [2013年第四届真题]剪格子 (C语言)
description: Q 1432 [2013 4th exam questions]Cut the grid (C Language)
date: '2020-02-11'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 1432: \[2013年第四届真题\]剪格子
时间限制: 1Sec 内存限制: 128MB
## 题目描述
```
历届试题  剪格子 
时间限制：1.0s     内存限制：256.0MB
    
问题描述
如下图所示，3  x  3  的格子中填写了一些整数。
+--*--+--+
|10*  1|52|
+--****--+
|20|30*  1|
*******--+
|  1|  2|  3|
+--+--+--+ 
我们沿着图中的星号线剪开，得到两个部分，每个部分的数字和都是60。
本题的要求就是请你编程判定：对给定的m  x  n  的格子中的整数，是否可以分割为两个部分，使得这两个区域的数字和相等。
如果存在多种解答，请输出包含左上角格子的那个区域包含的格子的最小数目。 
如果无法分割，则输出  0。
```
## 输入
程序先读入两个整数  m  n  用空格分割  (m,n< 10)。 
表示表格的宽度和高度。 
接下来是n行，每行m个正整数，用空格分开。每个整数不大于10000。
## 输出
输出一个整数，表示在所有解中，包含左上角的分割区可能包含的最小的格子数目。 
## 样例输入
```
3 3
10 1 52
20 30 1
1 2 3
```
## 样例输出
```
3
```
## C代码
```c
#include <stdio.h>
int a[10][10];//存值
int b[10][10];//标记数组
int count=100;
int m,n,sum=0;
int dx[4]={0,1,0,-1};
int dy[4]={1,0,-1,0};
void f(int s,int i,int j,int bs)
{   //s-> 当前和  i,j 当前点的坐标 ，bs  当前步数（格子数）
      if(s==sum/2&&count>bs)count=bs;//判断是否更新答案
      else{
  	     for(int k=0;k<4;k++){
  	 	  int x=dx[k]+i;
  	 	  int y=dy[k]+j;//边界判断和剪枝
  	 	   if(b[x][y]==1&&i>=0&&i<n&&j>=0&&j<m&&(s+a[x][y])<=sum/2){
  	 	     b[x][y]=0;  //此时a[0][0] 只作连接用 所以格子和值都不增加
			if(x==0&&y==0) f(s,x,y,bs);
			else f(s+a[x][y],x,y,bs+1);
		      b[x][y]=1;//消除标记
  	        }	
	     }
  	   }
}
int main()
{int i,j,tem;
scanf("%d%d",&m,&n);//输入宽、高 
for(i=0;i<n;i++)//注意坑点  先输入纵坐标的m 再输入的横坐标
for(j=0;j<m;j++)
{scanf("%d",&a[i][j]);//值
 sum+=a[i][j]; b[i][j]=1;//初始化标记数组
} 
 
if(sum%2==1)printf("0");//预判是否可以分两部分
else{ f(a[0][0],0,0,1);
    if(count!=100) printf("%d\n",count);
    else printf("0\n");
 }    
return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行