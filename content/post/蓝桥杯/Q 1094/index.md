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

# Q 1094: Input and output processing of strings
Time limit: 1Sec Memory Limit: 128MB
## Title Description
Input and output processing of strings.
## Input
The first line is a positive integer N, up to 100, followed by multiple lines (lines larger than N), each of which may contain spaces and no more than 1000 characters.
## Output
The first N lines of the input string (which may contain spaces) are output as is, and then the remaining strings (which do not contain spaces) are output sequentially by line with a space or carriage return division. A blank line is output between each line of output.
## Sample Input
```
2
www.dotcpp.com DOTCPP
A C M
D O T CPP
```
## Sample Output
```
www.dotcpp.com DOTCPP

A C M

D

O

T

CPP

```
## C Code
```c
 #include<stdio.h>
int main(){
    int N, i;
    scanf("%d", &N);
    getchar();    //Capture carriage return
    char str[N][1000];    //Used to save the first N lines of the string
    char extra[1000];    //Used to save additional strings
    for(i=0; i<N; i++){    //Loop through each string in a specified number of lines
        gets(str[i]);
    }
    for(i=0; scanf("%c", &extra[i]) != EOF; i++){
        //Enter additional strings, one character at a time, when the end of the input (ctrl+Z) input stops, the benefit in the line feed will not terminate the input
    }
    for(i=0; i<N; i++){
        printf("%s\n\n", str[i]);
    }
    for(i=0; extra[i] != NULL; i++){
        if(extra[i] == ' '||extra[i] == '\n'){    //Line break when there are spaces or line breaks in the extra array
            printf("\n\n");
            continue;
        }
        printf("%c", extra[i]);
    }
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.