---
title: Q 1427 [2014 5th exam questions] Dividing candy (C Language)
description: 题目 1427 [2014年第五届真题]分糖果 (C语言)
date: '2020-03-28'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1427: [2014 5th exam questions] Dividing candy
Time limit: 1Sec Memory Limit: 128MB
## Title Description
There are n children sitting in a circle. The teacher gives each child an even number of candies at random and then plays the following game:

Each child gives half of his or her candy to the child on his or her left hand side.

After one round of candy distribution, the child with the odd number of candies is given one additional candy by the teacher, thus making the number even.

Repeat this game until all the children have the same number of candies.

Your task is to predict the total number of candies that the teacher will need to give out given the known initial candy situation.
## Input
The program first reads in an integer N (2< N< 100), which represents the number of children. 
Then comes a line of N even numbers separated by spaces (each even number is not greater than 1000 and not less than 2) 
## Output
The program is asked to output an integer that represents the number of candies the teacher needs to make up.
## Sample Input
```
3 
2 2 4 
```
## Sample Output
```
4
```
## C Code
```c
#include<stdio.h>
int main()
{
    int a,i,j,k,sum=0;
    scanf("%d", &a);//Enter a few children
    int student[a];
    for(i=0;i<a;i++){
        scanf("%d",&student[i]);//The candy in each child's hand
    }
    while(1){
        j=1;//The other flag bit is 1, 0 means the condition is not met, need to be divided into candy
        for(i=0;i<a-1;i++){
            if(student[i]!=student[i+1]){
                j=0;//Once a bit is not the same, mark position 0 and jump out of the loop
                break;
            }
        }
        if(j==0){//If the conditions are not met, start dividing the candy
            int c=student[0]/2;//The first one will record the number of sweets and leave it to the last student, because they are sitting around together, so it is a cycle.
            for(i=0;i<a;i++){
                student[i]=student[i]/2;//The number of sweets for each student is halved
                if(i>=1){
                    student[i-1]+=student[i];//After adding the candy given by the next student from the 0 position, there is no one left to give candy to the last student, so the candy of one of our students can be given to him.
                }
            }
            student[a-1]+=c;//The last classmate's candy to him
            for(i=0;i<a;i++){//After dividing the candy if there is an odd number of candy in the hands of students, the teacher will give him one, +1, and let sum+1 record the number of candy given by the teacher, and finally output
                if(student[i]%2!=0){
                    sum++;//Records
                    student[i]++;//The teacher gave a candy, so +1.
                }
            }
        }
        else{
            printf("%d",sum);//If the condition is met, j will not be set to 0. After entering this output, brake will jump out of the while loop, and the whole function will be finished.
            break;
        }
    }
    return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.