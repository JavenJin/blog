---
title: 题目 1429 [2014年第五届真题]兰顿蚂蚁 (C语言)
description: Q 1429 [2014 5th exam questions] Landon Ants (C Language)
date: '2020-02-10'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1429: \[2014年第五届真题\]兰顿蚂蚁
时间限制: 1Sec 内存限制: 128MB
## 题目描述
![Landon Ants](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/%E8%93%9D%E6%A1%A5%E6%9D%AF/Q%201429/landon-ants.png)

兰顿蚂蚁，是于1986年，由克里斯·兰顿提出来的，属于细胞自动机的一种。


平面上的正方形格子被填上黑色或白色。在其中一格正方形内有一只“蚂蚁”。
蚂蚁的头部朝向为：上下左右其中一方。

蚂蚁的移动规则十分简单：
若蚂蚁在黑格，右转90度，将该格改为白格，并向前移一格；
若蚂蚁在白格，左转90度，将该格改为黑格，并向前移一格。

规则虽然简单，蚂蚁的行为却十分复杂。刚刚开始时留下的路线都会有接近对称，像是会重复，但不论起始状态如何，蚂蚁经过漫长的混乱活动后，会开辟出一条规则的“高速公路”。

蚂蚁的路线是很难事先预测的。

你的任务是根据初始状态，用计算机模拟兰顿蚂蚁在第n步行走后所处的位置。
## 输入
输入数据的第一行是  m  n  两个整数（3  <   m,  n  <   100），表示正方形格子的行数和列数。 
接下来是  m  行数据。 
每行数据为  n  个被空格分开的数字。0  表示白格，1  表示黑格。 

接下来是一行数据：x  y  s  k,  其中x  y为整数，表示蚂蚁所在行号和列号（行号从上到下增长，列号从左到右增长，都是从0开始编号）。s  是一个大写字母，表示蚂蚁头的朝向，我们约定：上下左右分别用：UDLR表示。k  表示蚂蚁走的步数。 
## 输出
输出数据为一个空格分开的整数  p  q,  分别表示蚂蚁在k步后，所处格子的行号和列号。
## 样例输入
```
5  6 
0  0  0  0  0  0 
0  0  0  0  0  0 
0  0  1  0  0  0 
0  0  0  0  0  0 
0  0  0  0  0  0 
2  3  L  5 
```
## 样例输出
```
1 3
```
## C代码
#### 解法A
```c
#include<stdio.h>
int main()
{
    int m,n,a[105][105],i,j,x,y,k;
    char s;
    scanf("%d%d",&m,&n);
    for(i=0;i<m;i++)
    for(j=0;j<n;j++)
    scanf("%d",&a[i][j]);
    scanf("%d%d %c%d",&x,&y,&s,&k);
    for(;k>0;k--)
    {
        if(s == 'U')
        {
            if(a[x][y] == 1)
            {
                s = 'R';
                a[x][y] = 0;
                y++;
            }
            else
            {
                s = 'L';
                a[x][y] = 1;
                y--;
            }
        }
        else if(s == 'D')
        {
            
            if(a[x][y] == 1)
            {
                s = 'L';
                a[x][y] = 0;
                y--;
            }
            else
            {
                s = 'R';
                a[x][y] = 1;
                y++;
            }
        }
        else if(s == 'L')
        {
            
            if(a[x][y] == 1)
            {
                s = 'U';
                a[x][y] = 0;
                x--;
            }
            else
            {
                s = 'D';
                a[x][y] = 1;
                x++;
            }
        }
        else
        {
            
            if(a[x][y] == 1)
            {
                s = 'D';
                a[x][y] = 0;
                x++;
            }
            else
            {
                s = 'U';
                a[x][y] = 1;
                x--;
            }
        }
    }
    printf("%d %d",x,y);
    return 0;
}
```
#### 解法B
```c
#include <stdio.h>
char d0[4]= {'L','U','R','D'};
char d1[4]= {'L','D','R','U'};
int main() {
	int x,y,k,m,n;
	char s;
	int i,j,maze[100][100];
	scanf("%d %d",&m,&n);
	for(i=0; i<m; i++)
		for(j=0; j<n; j++)
			scanf("%d",&maze[i][j]);
	scanf("%d %d %c %d",&x,&y,&s,&k);
	while(k--) {
		if(maze[x][y]) {
			maze[x][y]=0;
			for(i=0; i<4; i++)
				if(s==d0[i]) break;
			s=d0[(i+1)%4];
			switch(s) {
				case'L':
					y--;
					break;
				case'R':
					y++;
					break;
				case'U':
					x--;
					break;
				case'D':
					x++;
					break;
			}
		} else {
			maze[x][y]=1;
			for(i=0; i<4; i++)
				if(s==d1[i]) break;
			s=d1[(i+1)%4];
			switch(s) {
				case'L':
					y--;
					break;
				case'R':
					y++;
					break;
				case'U':
					x--;
					break;
				case'D':
					x++;
					break;
			}
		}
	}
	printf("%d %d\n",x,y);
	return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行