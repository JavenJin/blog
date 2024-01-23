---
title: Q 1429 [2014 5th exam questions] Landon Ants (C Language)
description: 题目 1429 [2014年第五届真题]兰顿蚂蚁 (C语言)
date: '2020-02-10'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Algorithm
---

# Q 1429: [2014 5th exam questions] Landon Ants
Time limit: 1Sec Memory Limit: 128MB
## Title Description
![Landon Ants](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/%E8%93%9D%E6%A1%A5%E6%9D%AF/Q%201429/landon-ants.png)

The Langdon ant, which was introduced in 1986 by Chris Langdon, is a type of cellular automaton.


A square grid on a flat surface is filled with black or white. In one of the squares there is an "ant".
The ant's head is oriented to one of the left and right sides.

The movement rule for ants is very simple:
If the ant is in a black square, turn 90 degrees to the right, change the square to a white square, and move forward one square;
If the ant is in the white frame, turn 90 degrees to the left, change the frame to black, and move one frame forward.

Although the rule is simple, the ant's behavior is very complicated. The routes left at the beginning will be close to symmetrical and seem to repeat, but regardless of the starting state, the ants will open up a regular "highway" after a long period of chaotic activity.

The route of ants is very difficult to predict in advance.

Your task is to use a computer to simulate the position of the Langdon ants after the nth walk, based on the initial state.
## Input
The first row of the input data is m n two integers (3 < m, n < 100), indicating the number of rows and columns of the square grid. 
This is followed by m rows of data. 
Each row of data is n numbers separated by spaces. 0 indicates a white cell and 1 indicates a black cell. 

Next is a row of data: x y s k, where x y is an integer that represents the row and column numbers of the ants (row numbers grow from top to bottom, column numbers grow from left to right, both starting from 0). s is a capital letter that represents the orientation of the ants' heads, and we agree to use: UDLR for top, bottom, left and right. k represents the number of steps taken by the ants. 
## Output
The output data is a space-separated integer p q, which represents the row and column numbers of the grid in which the ant is located after k steps, respectively.
## Sample Input
```
5  6 
0  0  0  0  0  0 
0  0  0  0  0  0 
0  0  1  0  0  0 
0  0  0  0  0  0 
0  0  0  0  0  0 
2  3  L  5 
```
## Sample Output
```
1 3
```
## C Code
#### Solution A
```c
#include<stdio.h>
int main()
{
    int m,n,a[105][105],i,j,x,y,k;
    char s;
    scanf("%d%d",&m,&n);
    for(i=0;i<m;i++)
    for(j=0;j<n;j++)
    scanf("%d",&a[i][j]);
    scanf("%d%d %c%d",&x,&y,&s,&k);
    for(;k>0;k--)
    {
        if(s == 'U')
        {
            if(a[x][y] == 1)
            {
                s = 'R';
                a[x][y] = 0;
                y++;
            }
            else
            {
                s = 'L';
                a[x][y] = 1;
                y--;
            }
        }
        else if(s == 'D')
        {
            
            if(a[x][y] == 1)
            {
                s = 'L';
                a[x][y] = 0;
                y--;
            }
            else
            {
                s = 'R';
                a[x][y] = 1;
                y++;
            }
        }
        else if(s == 'L')
        {
            
            if(a[x][y] == 1)
            {
                s = 'U';
                a[x][y] = 0;
                x--;
            }
            else
            {
                s = 'D';
                a[x][y] = 1;
                x++;
            }
        }
        else
        {
            
            if(a[x][y] == 1)
            {
                s = 'D';
                a[x][y] = 0;
                x++;
            }
            else
            {
                s = 'U';
                a[x][y] = 1;
                x--;
            }
        }
    }
    printf("%d %d",x,y);
    return 0;
}
```
#### Solution B
```c
#include <stdio.h>
char d0[4]= {'L','U','R','D'};
char d1[4]= {'L','D','R','U'};
int main() {
	int x,y,k,m,n;
	char s;
	int i,j,maze[100][100];
	scanf("%d %d",&m,&n);
	for(i=0; i<m; i++)
		for(j=0; j<n; j++)
			scanf("%d",&maze[i][j]);
	scanf("%d %d %c %d",&x,&y,&s,&k);
	while(k--) {
		if(maze[x][y]) {
			maze[x][y]=0;
			for(i=0; i<4; i++)
				if(s==d0[i]) break;
			s=d0[(i+1)%4];
			switch(s) {
				case'L':
					y--;
					break;
				case'R':
					y++;
					break;
				case'U':
					x--;
					break;
				case'D':
					x++;
					break;
			}
		} else {
			maze[x][y]=1;
			for(i=0; i<4; i++)
				if(s==d1[i]) break;
			s=d1[(i+1)%4];
			switch(s) {
				case'L':
					y--;
					break;
				case'R':
					y++;
					break;
				case'U':
					x--;
					break;
				case'D':
					x++;
					break;
			}
		}
	}
	printf("%d %d\n",x,y);
	return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.