---
title: Q 1084 Use the sieve method to find the prime numbers in N (C Language)
description: 题目 1084 用筛法求之N内的素数 (C语言)
date: '2020-02-14'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1084: Use the sieve method to find the prime numbers in N
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Use the sieve method to find the prime numbers in N.
## input
N
## Output
The prime numbers from 0 to N
## Sample Input
```
100
```
## Sample Output
```
2
3
5
7
11
13
17
19
23
29
31
37
41
43
47
53
59
61
67
71
73
79
83
89
97
```
## C Code
```c
#include<stdio.h>
int main()
{
    int n,i,j,k;
    scanf("%d",&n);
    for(i=2;i<=n;i++)
    {
        k=1;
        for(j=2;j<i;j++)
        {
            if(i%j == 0)
            k=0;
        }
        if(k==1)
        printf("%d\n",i);
    }

    int vio;
    scanf("%d",&vio);
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.