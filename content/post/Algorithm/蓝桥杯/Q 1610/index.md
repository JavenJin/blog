---
title: Q 1616 [Algorithm Improvement VIP]Passing Game (C Language)
description: 题目 1616 [算法提高VIP]传球游戏 (C语言)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# 题目 Q 1616: [Algorithm Improvement VIP]Passing Game
Time limit: 1Sec Memory Limit: 128MB
## Title Description
During physical education class, Barbara's teacher often takes the students to play games together. This time, the teacher took the students together to do the passing game.
The rules of the game are as follows: n students stand in a circle, one of the students holding a ball in his hand, when the teacher blows the whistle to start passing the ball, each student can pass the ball to one of his left and right two students (left and right arbitrarily), when the teacher blows the whistle again, the passing stops, at this time, the one holding the ball did not pass out is the loser, to give a show.
The clever Barbara asked an interesting question: how many different passing methods can make the ball start passing from Barbara's hand and return to Barbara's hand after passing m times. The two methods of passing the ball are treated as different methods when and only when the sequence of students who receive the ball in the order in which they receive it is different in both methods. For example, if there are 3 students #1, #2, and #3, and assuming Barbara is #1, there are 2 ways to return the ball to Barbara after 3 passes: 1-> 2-> 3-> 1 and 1-> 3-> 2-> 1.
## Input
A total of one line with two integers n, m separated by spaces (3< =n< =30, 1< =m< =30). 

Data size and conventions
100% of the data satisfy: 3< =n< =30, 1< =m< =30
## Output
t has a total of one line with an integer that indicates the number of methods that match the question. 
## Sample Input
```
3 3
```
## Sample Output
```
2
```
## C Code
```c
#include <stdio.h>
int n;
int main(){
    int at(int);
    int m,i,j,f[31][31] = {0};
    scanf("%d%d",&n,&m);
    f[1][2] = f[1][n] = 1;   //The 1st pass, #1 may only pass to #2 or #n
    for(i = 2;i <= m;i++)    //From the 2nd to the mth pass
    for(j = 1;j <= n;j++)    //The possibility of each pass to #1 to #n depends on the possibility of the last ball pass to the adjacent position
        f[i][j] = f[i - 1][at(j - 1)] + f[i - 1][at(j + 1)];
    printf("%d",f[m][1]);    //There are several possible ways to pass to #1 for the mth pass
    return 0;
}
int at(int x){               //Standing in a circle to pass the ball
    if(x<1) return x + n;    //When the number is reduced to 0, pass to number n
    if(x>n) return x - n;    //When the number increases to n+1, pass to number 1
    return x;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.