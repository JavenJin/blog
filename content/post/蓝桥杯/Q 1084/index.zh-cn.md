---
title: 题目 1084 用筛法求之N内的素数 (C语言)
description: Q 1084 Use the sieve method to find the prime numbers in N (C Language)
date: '2020-02-14'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1084: 用筛法求之N内的素数
时间限制: 1Sec 内存限制: 128MB
## 题目描述
用筛法求之N内的素数。
## 输入
N
## 输出
0～N的素数
## 样例输入
```
100
```
## 样例输出
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
## C代码
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
#### 通过[C语言网](https://www.dotcpp.com/)编译运行