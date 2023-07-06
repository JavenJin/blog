---
title: Q 1094 Input and output processing of strings (C Language)
description: 题目 1094 字符串的输入输出处理 (C语言)
date: '2018-11-02'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# 题目 1094: 字符串的输入输出处理
时间限制: 1Sec 内存限制: 128MB
## 题目描述
字符串的输入输出处理。
## 输入
第一行是一个正整数N，最大为100。之后是多行字符串（行数大于N）， 每一行字符串可能含有空格，字符数不超过1000。
## 输出
先将输入中的前N行字符串（可能含有空格）原样输出，再将余下的字符串（不含有空格）以空格或回车分割依次按行输出。每行输出之间输出一个空行。
## 样例输入
```
2
www.dotcpp.com DOTCPP
A C M
D O T CPP
```
## 样例输出
```
www.dotcpp.com DOTCPP

A C M

D

O

T

CPP

```
## C代码
```c
 #include<stdio.h>
int main(){
    int N, i;
    scanf("%d", &N);
    getchar();    //捕获回车
    char str[N][1000];    //用于保存前N行的字符串
    char extra[1000];    //用于保存额外的字符串
    for(i=0; i<N; i++){    //按规定行数循环输入每行字符串
        gets(str[i]);
    }
    for(i=0; scanf("%c", &extra[i]) != EOF; i++){
        //输入额外字符串，一个字符一个字符输入，当输入结尾时（ctrl+Z）输入停止，好处在换行不会终止输入
    }
    for(i=0; i<N; i++){
        printf("%s\n\n", str[i]);
    }
    for(i=0; extra[i] != NULL; i++){
        if(extra[i] == ' '||extra[i] == '\n'){    //当额外数组中有空格或换行符时换行
            printf("\n\n");
            continue;
        }
        printf("%c", extra[i]);
    }
    return 0;
}
```
#### 通过[C语言网](https://www.dotcpp.com/)编译运行