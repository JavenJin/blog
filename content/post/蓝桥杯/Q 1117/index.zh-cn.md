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

# 题目 1117: K-进制数
时间限制: 1Sec 内存限制: 128MB
## 题目描述

考虑包含N位数字的K-进制数. 定义一个数有效, 如果其K-进制表示不包含两连续的0.

例:
1010230 是有效的7位数
1000198 无效
0001235 不是7位数, 而是4位数.

给定两个数N和K, 要求计算包含N位数字的有效K-进制数的总数.

假设2 <= K <= 10; 2 <= N; 4 <= N+K <= 18.
## 输入
两个十进制整数N和K
## 输出
十进制表示的结果
## 样例输入
```
2
10
```
## 样例输出
```
90
```
## C代码
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
#### 通过[C语言网](https://www.dotcpp.com/)编译运行