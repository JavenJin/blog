---
title: Q 1157 Affinity number (C Language)
description: 题目 1157 亲和数 (C语言)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1157: Affinity number
Time limit: 1Sec Memory Limit: 128MB
## Title Description
In his study of natural numbers, the ancient Greek mathematician Pythagoras found that the sum of all the true covariates (i.e., covariates that are not themselves) of 220 is

1+2+4+5+10+11+20+22+44+55+110 = 284.

People are surprised by such a number and call it an affine number. Generally speaking, two numbers are affine if either of them is the sum of the true divisors of the other number.
Your task is to write a program that determines whether the given two numbers are affine numbers
## Input
The first line of the input data contains a number M, followed by M lines, one instance per line, containing two integers A,B; where 0 <= A,B <= 600000 .
## Output
For each test instance, output YES if A and B are affinity numbers, otherwise output NO.
## Sample Input
```
2
220 284
100 200
```
## Sample Output
```
YES
NO
```
## C Code
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
#### All through [C语言网](https://www.dotcpp.com/) compile and run.