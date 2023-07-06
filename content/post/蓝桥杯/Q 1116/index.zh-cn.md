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

# 题目 1116: IP判断
时间限制: 1Sec 内存限制: 128MB
## 题目描述
在基于Internet的程序中，我们常常需要判断一个IP字符串的合法性。
合法的IP是这样的形式：
A.B.C.D
其中A、B、C、D均为位于[0, 255]中的整数。为了简单起见，我们规定这四个整数中不允许有前导零存在，如001这种情况。
现在，请你来完成这个判断程序吧^_^
## 输入
输入由多行组成，每行是一个字符串，输入由“End of file”结束。
字符串长度最大为30，且不含空格和不可见字符
## 输出
对于每一个输入，单独输出一行
如果该字符串是合法的IP，输出Y，否则，输出N
## 样例输入
```
1.2.3.4
a.b.c.d
267.43.64.12
12.34.56.bb
210.43.64.129
-123.4.5.6
```
## 样例输出
```
Y
N
N
N
Y
N
```
## C代码
```c
#include<stdio.h>
#include<string.h>
int main()
{
    int a,b,c,d;
    int k;
    char s[100];
    char end[100]={"End of file"};//用于判断是否结束
    while(~(k=scanf("%d.%d.%d.%d",&a,&b,&c,&d)))
    {
        gets(s);
        if(strcmp(s,end)==0) return 0;//判断是否结束
        else if(s[0]!='\0') {printf("N\n");continue;} //有多余的字符串时直接打印N，并进行下一个
        if(k==4 && a>=0 && a<=255 && b>=0 && b<=255 && c>=0 && c<=255 && d>=0 && d<=255)//判断是否符合题意
        printf("Y\n");
        else
            printf("N\n");
        fflush(stdin);//清除缓冲区
    }
    return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行