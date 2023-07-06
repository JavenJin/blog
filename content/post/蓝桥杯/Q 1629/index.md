---
title: Q 1629 [Algorithm Training VIP]Water connection problems (C Language)
description: 题目 1629 [算法训练VIP]接水问题 (C语言)
date: '2020-03-21'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - 蓝桥杯
---

# Q 1629: [Algorithm Training VIP]Water connection problems
Time limit: 1Sec Memory Limit: 128MB
## Title Description
The school has a water room with a total of m faucets for students to turn on the water, each with an equal volume of water per second of 1.

Now there are n students ready to receive water, and their initial order of receiving water has been determined. The students are numbered from 1 to n in the order in which they receive water, and the amount of water received by student i is wi. At the beginning of the connection, students 1 to m each occupy a faucet and turn on the faucet at the same time to receive water. When one of the students, j, completes the required amount of water, the next student in line, k, immediately takes the place of j and starts to receive water. This changeover process is instantaneous and no water is wasted. That is, when student j finishes receiving water at the end of the xth second, student k immediately starts receiving water at the xth+1st second. If the current number of water connections n' is less than m, then only n' taps are supplied and the other m-n' taps are closed.

Now, given the amount of water received by n students, ask how many seconds it takes for all students to finish receiving water according to the above rules.
## Input
Row 1 has two integers n and m, separated by a space, indicating the number of persons receiving water and the number of faucets, respectively.
Row 2 has n integers w1, w2, ......, wn, separated by a space between each integer, and wi represents the amount of water received by student i.
1 ≤ n ≤ 10000，1 ≤ m ≤ 100 且 m ≤ n；
1 ≤ wi ≤ 100。
## Output
The output is a single line, 1 integer, indicating the total time required to pick up the water.
## Sample Input
```
5 3
4 4 1 2 1
```
## Sample Output
```
4
```
## C Code
```c
#include <stdio.h>
int dm[101]={0};
int w[10001];
int t=1;
int bj=0;
int main()
{
	int n,m,i,j,d=1;
	scanf("%d%d",&n,&m);
	for(i=1;i<=n;i++)
	scanf("%d",&w[i]);
	while(1)
	{
		for(i=1;i<=m;i++)
		{
			if(dm[i]==0)//若有水龙头 这一单位时间 没使用 则替换 接水者 
			{
				if(d<=n)dm[i]=d++;//dm[i]  i 代表 水龙头 编号 dm[i]存储 这一单位时间 接水人编号 
			}
			if(dm[i]!=0)//水龙头有人接水  本水龙头接水人节水量-1 
			{
				w[dm[i]]-=1; if(w[dm[i]]==0)dm[i]=0;bj=1;}//这一单位本水龙头接水人接水量为0则空出水龙头
			}
			if(bj!=1)
				break; //bj==1则表示 本次单位时间 有水龙头使用 bj==0则标记本单位时间没水龙头使用则所有过程上一秒已完成   
			bj=0;
			t++;
		}
	printf("%d\n",t-1);
	return 0;
}
```
#### All through [C语言网](https://www.dotcpp.com/) compile and run.