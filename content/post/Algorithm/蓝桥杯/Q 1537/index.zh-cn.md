---
title: 题目 1537 [算法提高VIP]栅格打印问题 (C语言)
description: Q 1537 [Algorithm Improvement VIP]Raster printing problems (C Language)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 1537: \[算法提高VIP\]栅格打印问题
时间限制: 1Sec 内存限制: 128MB
## 题目描述
编写一个程序，输入两个整数，作为栅格的高度和宽度，然后用“+”、“-”和“|”这三个字符来打印一个栅格。
## 输入
输入只有一行，包括两个整数，分别为栅格的高度和宽度。
## 输出
输出相应的栅格。 
## 样例输入
```
3 2
```
## 样例输出
```
+-+-+
| | |
+-+-+
| | |
+-+-+
| | |
+-+-+
```
## C代码
```c
#include<stdio.h>
int main()
{
    int L,H;
    int i,j;
    while(scanf("%d%d",&H,&L)!=EOF)
    {
        if(H<=0||L<=0) break;//小提示：有道友没过就是没加类似判断（本人第一次没加也没过）
        for(i=0;i<H;i++)
        {
            for(j=0;j<=L;j++)
            {
                if(j!=L)
                    printf("+-");
                else putchar('+');
            }
            putchar('\n');
            for(j=0;j<=L;j++)
            {
                if(j!=L)
                    printf("| ");
                else putchar('|');
            }
            putchar('\n');
        }
        for(j=0;j<=L;j++)//封底
        {
            if(j!=L)
                printf("+-");
            else putchar('+');
        }
        putchar('\n');
    }
    return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行