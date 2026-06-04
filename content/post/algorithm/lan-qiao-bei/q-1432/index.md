---
title: Q 1432 [2013 4th exam questions]Cut the grid (C Language)
description: 题目 1432 [2013年第四届真题]剪格子 (C语言)
date: '2020-02-11'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1432: [2013 4th exam questions]Cut the grid
Time limit: 1Sec Memory Limit: 128MB
## Title Description
```
Past exams
Cut the grid 
Time limit: 1.0s  Memory limit: 256.0MB
    
Problem Description
As shown in the figure below, the grid of 3 x 3 is filled with some integers.
+--*--+--+
|10*  1|52|
+--****--+
|20|30*  1|
*******--+
|  1|  2|  3|
+--+--+--+ 
We cut along the asterisk line in the figure to get two parts, each with a sum of numbers of 60.
The question asks you to programmatically determine whether the integer in the given m x n lattice can be partitioned into two parts such that the sum of the numbers in these two regions is equal.
If there are multiple solutions, output the minimum number of squares contained in the region containing the top left square. 
If it cannot be divided, output 0.
```
## Input
The program first reads in two integers m n divided by spaces (m,n< 10). 
This represents the width and height of the table. 
Next are n rows of m positive integers each, separated by spaces. Each integer is not greater than 10000.
## Output
Output an integer indicating the smallest number of cells that the partition containing the upper-left corner may contain among all solutions. 
## Sample Input
```
3 3
10 1 52
20 30 1
1 2 3
```
## Sample Output
```
3
```
## C Code
```c
#include <stdio.h>
int a[10][10];//Save value
int b[10][10];//Tagging arrays
int count=100;
int m,n,sum=0;
int dx[4]={0,1,0,-1};
int dy[4]={1,0,-1,0};
void f(int s,int i,int j,int bs)
{   //s-> current and i,j coordinates of the current point , bs current number of steps (number of grids)
      if(s==sum/2&&count>bs)count=bs;//Determine if the answer is updated
      else{
  	     for(int k=0;k<4;k++){
  	 	  int x=dx[k]+i;
  	 	  int y=dy[k]+j;//Boundary judgment and pruning
  	 	   if(b[x][y]==1&&i>=0&&i<n&&j>=0&&j<m&&(s+a[x][y])<=sum/2){
  	 	     b[x][y]=0;  //At this point, a[0][0] is only used for concatenation, so neither the grid nor the value is increased.
			if(x==0&&y==0) f(s,x,y,bs);
			else f(s+a[x][y],x,y,bs+1);
		      b[x][y]=1;//Elimination of markers
  	        }	
	     }
  	   }
}
int main()
{int i,j,tem;
scanf("%d%d",&m,&n);//Input width and height 
for(i=0;i<n;i++)//Note that the pit point is entered first in the vertical coordinate m and then in the horizontal coordinate
for(j=0;j<m;j++)
{scanf("%d",&a[i][j]);//Value
 sum+=a[i][j]; b[i][j]=1;//Initializing the tag array
} 
 
if(sum%2==1)printf("0");//Can pre-judgment be divided into two parts
else{ f(a[0][0],0,0,1);
    if(count!=100) printf("%d\n",count);
    else printf("0\n");
 }    
return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.