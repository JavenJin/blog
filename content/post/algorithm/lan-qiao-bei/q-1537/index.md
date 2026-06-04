---
title: Q 1537 [Algorithm Improvement VIP]Raster printing problems (C Language)
description: 题目 1537 [算法提高VIP]栅格打印问题 (C语言)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1537: [Algorithm Improvement VIP]Raster printing problems
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Write a program that enters two integers as the height and width of a grid, and then prints a grid using the characters "+", "-" and "|".
## Input
The input has only one line and consists of two integers, which are the height and width of the grid.
## Output
Output the corresponding raster. 
## Sample Input
```
3 2
```
## Sample Output
```
+-+-+
| | |
+-+-+
| | |
+-+-+
| | |
+-+-+
```
## C Code
```c
#include<stdio.h>
int main()
{
    int L,H;
    int i,j;
    while(scanf("%d%d",&H,&L)!=EOF)
    {
        if(H<=0||L<=0) break;//Tip: some of you did not pass is not added similar judgment (I did not add the first time also did not pass)
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
        for(j=0;j<=L;j++)//Back cover
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
#### All through [C语言网](https://www.dotcpp.com/) compile and run.