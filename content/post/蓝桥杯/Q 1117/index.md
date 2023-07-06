---
title: Q 1117 K-Decimal number (C Language)
description: 题目 1117 K-进制数 (C语言)
date: '2020-02-05'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1117: K-Decimal number
Time limit: 1Sec Memory Limit: 128MB
## Title Description

Consider a K-decimal number containing N digits. Define a number to be valid if its K-decimal representation does not contain two consecutive zeros.

Example.
1010230 is a valid 7-digit number
1000198 is invalid
0001235 is not a 7-digit number, but a 4-digit number.

Given two numbers N and K, calculate the total number of valid K-digit numbers that contain N digits.

Assume that 2 <= K <= 10; 2 <= N; 4 <= N+K <= 18.
## Input
Two decimal integers N and K
## Output
Decimal representation of the result
## Sample Input
```
2
10
```
## Sample Output
```
90
```
## C Code
```c
#include<stdio.h>
int a[20],n,k;
int cnt;
void dfs(int s)
{
    if(s==n)
    {
        cnt++;
        return;
    }
    for(int i=0; i<k; i++)
    {
        if((s==0&&i==0)||(s>0&&i==0&&a[s-1]==0))
            continue;
        a[s]=i;
        dfs(s+1);
    }
}
int main()
{
    scanf("%d%d",&n,&k);
    cnt=0;
    dfs(0);
    printf("%d\n",cnt);
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.