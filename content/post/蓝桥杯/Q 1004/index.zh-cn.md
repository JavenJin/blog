---
title: 题目 1004 [递归]母牛的故事 (C语言)
description: Q 1004 [Recursive] The story of the cow (C Language)
date: '2018-11-02'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1004: \[递归\]母牛的故事
时间限制: 1Sec 内存限制: 128MB
## 题目描述
有一头母牛，它每年年初生一头小母牛。每头小母牛从第四个年头开始，每年年初也生一头小母牛。请编程实现在第n年的时候，共有多少头母牛？
## 输入
输入数据由多个测试实例组成，每个测试实例占一行，包括一个整数n(0<n<55)，n的含义如题目中描述。
n=0表示输入数据的结束，不做处理。
## 输出
对于每个测试实例，输出在第n年的时候母牛的数量。
每个输出占一行。
## 样例输入
2
4
5
0
## 样例输出
2
4
6
## C代码
#### 解法A

```c
#include<stdio.h>
int main()
{
    int sum[60],n[60],i,j;
    
	sum[1]=1;
	sum[2]=2;
	sum[3]=3;
	for(i=4;i<=55;i++)
	{
		sum[i]=sum[i-1]+sum[i-3];
	}
    
    i=0;
    do
    {
    	scanf("%d",&n[i]);
    	i++;
	}while(n[i-1]);
	
	for(j=i;j>1;j--)
	{
		printf("%d",sum[n[i-j]]);
		printf("\n");
	}
	
    return 0;
}
```

#### 解法B

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
	int i, t;
	while(scanf("%d", &t) != EOF)
	{
		if(t == 0) 
			return 0;
		else
		{
			int s[60];
			s[0] = 1;
			s[1] = 2;
			s[2] = 3;
			for(i = 3; i < t; i++)
			{
				s[i] = s[i - 1] + s[i - 3];
			}
			printf("%d\n", s[t - 1]);
		}
	}
	return 0;
}
```
#### 均通过[C语言网](https://www.dotcpp.com/)编译运行