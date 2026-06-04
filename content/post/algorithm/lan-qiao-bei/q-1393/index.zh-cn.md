---
title: 题目 1393 钟神赛车 (C语言)
description: Q 1393 Bell God Racing (C Language)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 1393: 钟神赛车
时间限制: 1Sec 内存限制: 128MB
## 题目描述
钟神近来编码劳累，想骑车风光一番，于是找某君骑自行车比赛。已知某君和钟神的每辆自行车的速度，钟神赢一场得50银两银子，输一场赔50银两，平局不挣也不赔。钟神可以随意安排高中低档自行车的出场数序，假设钟神体力无限无损耗求钟神最多能挣多少钱
## 输入
多行测试数据，每行包含一个整数n和2n个32位正整数，第一个n表示自行车的数量，之后的n个32位整数表示某君自行车的速度，最后的n个32位整数表示钟神的自行车的速度
## 输出
钟神可以随意安排自行车的出场数序。输出钟神最多能挣多少钱，结果一定在32位整数的范围内
## 样例输入
```
3 2 1 3 2 2 3
3 2 1 3 1 1 3
```
## 样例输出
```
50
0
```
## C代码
```c
#include<stdio.h>  
void pai(int  *a,int n)
{
	int i,j,x;
	for(i=1;i<=n;i++)
	{
		for(j=0;j<n-1;j++)
		{
			if(a[j]<a[j+1])
			{
				x=a[j];a[j]=a[j+1];a[j+1]=x;
			}
		}
	} 
}

int main()  
{  
	int t[1000+22],q[1000+22]; 
    int n,i,j,k,s,win,lose;  
    while(scanf("%d",&n)!=EOF)  
    {  
		k=0;win=0,lose=0;  
        for(i=0;i<n;i++)
			scanf("%d",&q[i]);
        for(i=0;i<n;i++)
			scanf("%d",&t[i]);  
        pai(q,n);pai(t,n);
		while(k<n)
		{
			for(i=0;i<n-k;i++)
			{
				if(t[0]>q[i])
				{
					for(s=0;s<n-k-1;s++)
						t[s]=t[s+1];
					for(s=i;s<n-k-1;s++)
						q[s]=q[s+1];
					k++;
					win++;
					break;
				}
				else if((i==n-k-1)&&t[0]==q[i])
				{
					for(s=0;s<n-k-1;s++)
						t[s]=t[s+1];
					k++;
					break;
				}
				else if((i==n-k-1)&&t[0]<q[i])
				{
					lose=i+1;
					k=n;
					break;
				}
			}
		}
		printf("%d\n",50*(win-lose));  
    }
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行