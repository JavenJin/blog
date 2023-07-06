---
title: Q 1116 IP Judgment (C Language)
description: 题目 1094 IP判断 (C语言)
date: '2018-12-01'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1116: IP Judgment
Time limit: 1Sec Memory Limit: 128MB
## Title Description
In Internet-based programs, we often need to determine the legitimacy of an IP string.
A legitimate IP is of the form:
A.B.C.D
where A, B, C, and D are all integers located in [0, 255]. For simplicity, we specify that no leading zeros are allowed to exist in these four integers, as in the case of 001.
Now, please complete this judgment procedure ^_^
## Input
The input consists of multiple lines, each line is a string and the input is terminated by "End of file".
The maximum string length is 30, without spaces and invisible characters.
## Output
For each input, output a separate line
If the string is a legitimate IP, output Y, otherwise, output N
## Sample Input
```
1.2.3.4
a.b.c.d
267.43.64.12
12.34.56.bb
210.43.64.129
-123.4.5.6
```
## Sample Output
```
Y
N
N
N
Y
N
```
## C Code
```c
#include<stdio.h>
#include<string.h>
int main()
{
    int a,b,c,d;
    int k;
    char s[100];
    char end[100]={"End of file"};//Used to determine if the end
    while(~(k=scanf("%d.%d.%d.%d",&a,&b,&c,&d)))
    {
        gets(s);
        if(strcmp(s,end)==0) return 0;//Determine if the end
        else if(s[0]!='\0') {printf("N\n");continue;} //Print N directly when there are extra strings, and proceed to the next
        if(k==4 && a>=0 && a<=255 && b>=0 && b<=255 && c>=0 && c<=255 && d>=0 && d<=255)//Determine if it fits the question
        printf("Y\n");
        else
            printf("N\n");
        fflush(stdin);//Clear buffer
    }
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.