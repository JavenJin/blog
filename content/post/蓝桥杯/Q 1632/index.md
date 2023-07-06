---
title: Q 1632 [Algorithm Improvement VIP]Number of pairs (C Language)
description: 题目 1632 [算法提高VIP]数对 (C语言)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1632: [Algorithm Improvement VIP]Number of pairs
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Write a program that reads in an integer from the user and then lists all pairs of numbers, the product of each pair being the number.
## Input
The input has only one line, i.e. an integer. 
## Output
The output has several lines, each line is a multiplication equation. (Note: there is a space between the operator symbol and the number)
## Sample Input
```
32 
```
## Sample Output
```
1 * 32 = 32
2 * 16 = 32
4 * 8 = 32
8 * 4 = 32
16 * 2 = 32
32 * 1 = 32
```
## C Code
```c
#include<stdio.h>
int main(){
    int i,n;
    scanf("%d",&n);
    for(i=1;i<=n;i++){
        if(n%i==0)printf("%d * %d = %d\n",i,n/i,n);
    }
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.