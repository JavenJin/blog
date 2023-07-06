---
title: Q 1157 Affinity number (C Language)
description: 题目 1157 亲和数 (C语言)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1157: 亲和数
时间限制: 1Sec 内存限制: 128MB
## 题目描述
古希腊数学家毕达哥拉斯在自然数研究中发现，220的所有真约数(即不是自身的约数)之和为：

1+2+4+5+10+11+20+22+44+55+110＝284。

而284的所有真约数为1、2、4、71、 142，加起来恰好为220。人们对这样的数感到很惊奇，并称之为亲和数。一般地讲，如果两个数中任何一个数都是另一个数的真约数之和，则这两个数就是亲和数。
你的任务就编写一个程序，判断给定的两个数是否是亲和数
## 输入
输入数据第一行包含一个数M，接下有M行，每行一个实例,包含两个整数A,B； 其中 0 ＜＝A,B ＜＝600000 ;
## 输出
对于每个测试实例，如果A和B是亲和数的话输出YES，否则输出NO。
## 样例输入
```
2
220 284
100 200
```
## 样例输出
```
YES
NO
```
## C代码
```c
#include<stdio.h>
int main()
{
	int M,m,a[10000],b[10000],c[10000],sum_a,sum_b,j;
	scanf("%d",&M); 
	m = M;
	while(m)
	{
		scanf("%d%d",&a[m],&b[m]);
		m--;
	}
	for(m=1;m<=M;m++)
	{
		sum_a = 0;
		sum_b = 0;
		for(j=1;j<a[m];j++)
		{
			if(a[m]%j == 0)
				sum_a+=j;
		}
		for(j=1;j<b[m];j++)
		{
			if(b[m]%j == 0)
				sum_b+=j;
		}
//		printf("a=%d\tb=%d\n",a[m],b[m]);
//		printf("suma=%d\tsumb=%d",sum_a,sum_b);
		if((sum_a==b[m])&&(sum_b==a[m]))
			c[m]=1;
		else
			c[m]=0;
//		printf("\n%d",c[m]);
	}
	for(j=M;j>=1;j--)
	{
		if(c[j]==1)
			printf("YES\n");
		else
			printf("NO\n");
	}
	return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行