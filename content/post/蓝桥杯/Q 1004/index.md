---
title: Q 1004 [Recursive] The story of the cow (C Language)
description: 题目 1004 [递归]母牛的故事 (C语言)
date: '2018-11-02'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1004: \[Recursive\] The story of the cow
Time limit: 1Sec Memory Limit: 128MB
## Title Description
There is a cow that gives birth to a heifer at the beginning of each year. Each heifer also gives birth to one heifer at the beginning of each year, starting from the fourth year. Program how many heifers are there in year n?
## Input
The input data consists of multiple test instances, each of which occupies one line and includes an integer n (0<n<55), with n meaning as described in the title.
n=0 indicates the end of the input data and is not processed.
## Output
For each test instance, the number of cows at year n is output.
Each output occupies one line.
## Sample Input
2
4
5
0
## Sample Output
2
4
6
## C Code
#### Solution A

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

#### Solution B

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
#### All through [C语言网](https://www.dotcpp.com/) compile and run.