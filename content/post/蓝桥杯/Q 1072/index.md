---
title: Q 1072 Soda bottles (C Language)
description: 题目 1072 汽水瓶 (C语言)
date: '2020-07-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1072: Soda bottles
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Here's a question: "A store says that three empty soda bottles can be exchanged for one bottle of soda. Zhang has ten empty soda bottles in her hand, how many bottles of soda can she drink at most?" The answer is 5 bottles, the method is as follows: first 9 empty bottles for 3 bottles of soda, drink 3 full bottles, drink 4 empty bottles, with 3 and then a bottle, drink this full bottle, which is left 2 empty bottles. Then you let the boss first lend you a bottle of soda, drink the full bottle, drink the full bottle after the 3 empty bottles for a full bottle back to the boss. If Zhang has n empty soda bottles on hand, what is the maximum number of sodas he can exchange?
## input
The input file contains up to 10 sets of test data, each taking up one line and containing only one positive integer n (1<=n<=100), indicating the number of empty soda bottles in Zhang's hand. n=0 means the input is finished and your program should not process this line.
## Output
For each set of test data, output a line indicating the maximum number of soda bottles that can be drunk. If you can't drink one bottle, output 0.
## Sample Input
```
3
10
81
0
```
## Sample Output
```
1
5
40
```
## C Code
```c
#include <stdio.h>
int drink(int k)
{
    int s = 0, d = 0;
    while(s != 2 && s != 1){
    s = k%3 + k/3;
    d += k/3;
    k = s;
    }
    if(s == 2) return ++d;
    else return d;
}
int main(void)
{
    int n, i=0;
    int a[100];
    while(scanf("%d",&n)){
        if( n == 0) break;
        a[i] = drink(n);
        i++;
    }
    for(int j=0;j<i;j++) printf("%d\n",a[j]);
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.