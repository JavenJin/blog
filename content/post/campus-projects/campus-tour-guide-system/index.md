---
title: Campus tour guide system (pure C implementation) Shortest path - Dijkstra algorithm
description: 校园导游系统（纯C语言实现）最短路径 - Dijkstra算法
date: '2019-11-27'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
    - Dijkstra
---
#### Xijing University Tour Guide System

Learn data structures + C implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include <graphics.h>

      
#define MaxViewNum 50      /*Maximum number of attractions 50*/
#define MaxRoad 10000      /*Define the path to infinity*/

typedef int dist[MaxViewNum];
typedef int path[MaxViewNum];

//Define three structures to represent the contents of the diagram 
typedef struct
{
    char name[30];          /*Name of the attractions*/
    char introduce[200];    /*Attractions info*/	
    int  x,y;               /*Coordinates of attractions*/ 
}JDXX;                      /*Attractions Information*/

typedef struct
{
    JDXX jd[MaxViewNum];                 /*A one-dimensional array of vertices, the zero cell of the array is not used*/
    int length[MaxViewNum][MaxViewNum];  /*Storage path length*/
}MGraph;

MGraph M;                               /*Global variable, define M as MGraph type*/
int N=0;                                /*Global variable, number of current attractions*/ 
path p;
dist d;

void init()
{
    int i,j;
    strcpy(M.jd[1].name,"North Gate");
    strcpy(M.jd[1].introduce,"Located on Xijing Road, adjacent to the living area, convenient for shopping and transportation");
    strcpy(M.jd[2].name,"Art Boat");
    strcpy(M.jd[2].introduce,"Situated on Guihu Lake, leading to the paradise of art");
    strcpy(M.jd[3].name,"Flower Street");
    strcpy(M.jd[3].introduce,"With the s-shaped flower bed as the background, flowers bloom all year round");
    strcpy(M.jd[4].name,"Science Court");
    strcpy(M.jd[4].introduce,"Provide space for students to take English listening, computer classes, etc."); 
    strcpy(M.jd[5].name,"Piazza");
    strcpy(M.jd[5].introduce,"Including Bonang National Flag Times Square, which provides recreational activities for students");
    strcpy(M.jd[6].name,"Academic Building");
    strcpy(M.jd[6].introduce,"The place where students have their daily classes, the hall of knowledge");
    strcpy(M.jd[7].name,"Engineering Boat");
    strcpy(M.jd[7].introduce,"Provide students with space for experiments, practical training and study");
    strcpy(M.jd[8].name,"Library");
    strcpy(M.jd[8].introduce,"An environment with a strong cultural heritage for students to read and study quietly");
    strcpy(M.jd[9].name,"Apartment Building");
    strcpy(M.jd[9].introduce,"11--18 apartment buildings");
    strcpy(M.jd[10].name,"Center for College Student Development and Services");
    strcpy(M.jd[10].introduce,"Office locations of each school, providing one-stop services for students");
    strcpy(M.jd[11].name,"Puratos Restaurant");
    strcpy(M.jd[11].introduce,"Four floors of dining hall, providing three meals a day for students");
    strcpy(M.jd[12].name,"Jing Hua Grand Hall");
    strcpy(M.jd[12].introduce,"The largest auditorium in the school");
    strcpy(M.jd[13].name,"Gymnasium");
    strcpy(M.jd[13].introduce,"Provide a place for students to play indoor sports");
    strcpy(M.jd[14].name,"Scientific Research Building");
    strcpy(M.jd[14].introduce,"A place to conduct scientific research");
    strcpy(M.jd[15].name,"South playground");
    strcpy(M.jd[15].introduce,"Students brush sports software in the evening");
    strcpy(M.jd[16].name,"South Lake");
    strcpy(M.jd[16].introduce,"Also known as the Lake of Smiles, the lights are very beautiful at night");
    strcpy(M.jd[17].name,"South Gate");
    strcpy(M.jd[17].introduce,"Conveniently located on Shenhe 2nd Road");
    for(i=1;i<=MaxViewNum;i++)
	{
		for(j=1;j<=MaxViewNum;j++)
        {
			M.length[i][j]=MaxRoad;
        }
    }
    for(i=1;i<=MaxViewNum;i++)
    M.length[i][i]=0;
    M.length[1][2]=M.length[2][1]=30;
    M.length[1][3]=M.length[3][1]=30;
    M.length[2][3]=M.length[3][2]=30;
    M.length[2][4]=M.length[4][2]=70;
    M.length[3][5]=M.length[5][3]=30;
    M.length[3][6]=M.length[6][3]=50;
    M.length[4][5]=M.length[5][4]=50;
    M.length[4][7]=M.length[7][4]=100;
    M.length[5][6]=M.length[6][5]=30;
    M.length[6][7]=M.length[7][6]=100;
    M.length[6][10]=M.length[10][6]=20;
    M.length[7][8]=M.length[8][7]=30;
    M.length[7][9]=M.length[9][7]=30;
    M.length[7][10]=M.length[10][7]=30;
    M.length[8][9]=M.length[9][8]=30;
    M.length[9][10]=M.length[10][9]=50;
    M.length[9][11]=M.length[11][9]=30;
    M.length[10][11]=M.length[11][10]=30;
    M.length[11][12]=M.length[12][11]=100;
    M.length[11][13]=M.length[13][11]=50;
    M.length[12][13]=M.length[13][12]=50;
    M.length[12][15]=M.length[15][12]=30;
    M.length[12][17]=M.length[17][12]=150;
    M.length[13][14]=M.length[14][13]=70;
    M.length[13][15]=M.length[15][13]=30;
    M.length[13][16]=M.length[16][13]=50;
    M.length[14][16]=M.length[16][14]=50;
    M.length[15][16]=M.length[16][15]=20;
    M.length[16][17]=M.length[17][16]=30;
    N=17;
    M.jd[1].x=50;
    M.jd[1].y=25;
    M.jd[2].x=150;
    M.jd[2].y=125;
    M.jd[3].x=250;
    M.jd[3].y=25;
    M.jd[4].x=150;
    M.jd[4].y=475;
    M.jd[5].x=350;
    M.jd[5].y=175;
    M.jd[6].x=475;
    M.jd[6].y=50;
    M.jd[7].x=475;
    M.jd[7].y=475;
    M.jd[8].x=575;
    M.jd[8].y=650;
    M.jd[9].x=675;
    M.jd[9].y=525;
    M.jd[10].x=575;
    M.jd[10].y=150;
    M.jd[11].x=750;
    M.jd[11].y=225;
    M.jd[12].x=575;
    M.jd[12].y=525;
    M.jd[13].x=575;
    M.jd[13].y=225;
    M.jd[14].x=1075;
    M.jd[14].y=25;
    M.jd[15].x=1000;
    M.jd[15].y=375;
    M.jd[16].x=1100;
    M.jd[16].y=225;
    M.jd[17].x=1175;Attraction
    M.jd[17].y=325;
}

void scsyjd()
{
	int t;
	printf("All sites are as follows:\n"); 
	for(t=1;t<=N;t++)
	{
		printf("Number:%d\n   Attraction:%s\n   Introduction:%s\n",t,M.jd[t].name,M.jd[t].introduce);
	}
	printf("\nPress any key to return!");
	getch();
}

void zengj()
{  char s1[30],s2[200];    //Attraction Name; Attraction Introduction 
   int t,i,q,p,x,y;        //t is the number of Attraction connected to the Attraction; i is the number of Attraction that should be connected to it;
                           //q is the Attraction connected to it; p is the distance between this Attraction and the new Attraction 
                           //x is the x value at the Attraction position; y is the y value at the Attraction position 
   N++;  
   printf("Please enter the Name of this Attraction:");                 
   scanf("%s",&s1);
   printf("Please enter the Introduction of this Attraction:");
   scanf("%s",&s2);
   printf("Please enter the x value of the location of this Attraction:");
   scanf("%d",&x); 
   printf("Please enter the y value for the location of this Attraction:");
   scanf("%d",&y);
   strcpy(M.jd[N].name,s1);
   strcpy(M.jd[N].introduce,s2);
   M.jd[N].x=x;
   M.jd[N].y=y;
   printf("Please enter how many Attraction are connected to this Attraction:");
   scanf("%d",&t);
   for(i=1;i<=t;i++)
   {  printf("The %d Attraction is connected to it;",i);
      scanf("%d",&q);
      printf("The distance between them is:");
      scanf("%d",&p);
      M.length[N][q]=M.length[q][N]=p;
	}
	printf("\nPress any key to return!");
	getch();
}

void scjd()
{
	printf("Please enter the number of Attraction serial numbers to be deleted");
	int t,p,Q;
	scanf("%d",&p);
	Q=p;
	if(p<=N)
	{
	for(t=1;t<=N;t++)
	for(p=p;p<=N;p++)
		{
		M.length[t][p]=M.length[t][p+1];
		M.length[p][t]=M.length[p+1][t];		 
		}
	for(Q;Q<N;Q++)
	M.jd[Q]=M.jd[Q+1];
	printf("Deleted successfullyO(∩_∩)O");
	}
else
printf("Failed to delete←_←");
N--;
printf("\nPress any key to return!");	
getch();
}

void gxjd()
{
	int t;
	char s1[30],s2[200];
	printf("Please enter the Attraction Number to be updated:");
	scanf("%d",&t);
	if(t>N)
	printf("This Attraction does not exist, update failed");
	else
	{
		printf("Please enter Attraction Name:");
		scanf("%s",&s1);
		printf("Please enter Attraction Introduction:");
		scanf("%s",&s2);
		strcpy(M.jd[t].name,s1);
		strcpy(M.jd[t].introduce,s2);
		printf("Update complete!"); 
	}
	printf("\nPress any key to return!");
	getch();
}

void zengjl()
{
	int a,b,c; 
	printf("Please add a path between those two Attraction\n");
	printf("Please enter the first Attraction Number:");
	scanf("%d",&a);
	printf("Please enter the second Attraction Number:");
	scanf("%d",&b);
	printf("Please enter the length of this road:");
	scanf("%d",&c);
	if(a>N||b>N)
	printf("Attraction is out of range of existing Attraction, path addition failed!");
	else
	{
		M.length[a][b]=M.length[b][a]=c;
		printf("Path increase success!"); 
	} 
	printf("\nPress any key to return！");
	getch();
}

void scl()
{
	int a,b; 
	printf("Please remove the path between the two Attraction\n");
	printf("Please enter the first Attraction Number:");
	scanf("%d",&a);
	printf("Please enter the second Attraction Number:");
	scanf("%d",&b);
	if(a>N||b>N)
	printf("Attraction is out of range of existing Attraction, path deletion failed!");
	else
	{
		M.length[a][b]=M.length[b][a]=MaxRoad;
		printf("Path deleted successfully!"); 
	} 
	printf("\nPress any key to return!");
	getch();
}

void gxl()
{
	int a,b,c; 
	printf("Please update the road between the two Attraction\n");
	printf("Please enter the first Attraction Number:");
	scanf("%d",&a);
	printf("Please enter the second Attraction Number:");
	scanf("%d",&b);
	printf("Please enter the updated length:");
	scanf("%d",&c);
	if(a>N||b>N)
	printf("This path does not exist, path update failed!");
	else
	{
		M.length[a][b]=M.length[b][a]=c;
		printf("Path updated successfully!"); 
	} 
	printf("\nPress any key to return!");
	getch();
}

void cxjd()
{
	int a;
	printf("The Attraction Number you are looking for is:");
	scanf("%d",&a);
	if(a>N)
	printf("The Attraction of the query does not exist, the query failed!"); 
	else
	printf("Number:%d\n   Attraction:%s\n   Introduction:%s\n",a,M.jd[a].name,M.jd[a].introduce);
	printf("\nPress any key to return!"); 
	getch();
}

void dijkstra_syjd()
{
	int v0;
	printf("Please enter the Attraction of your query:");
	scanf("%d",&v0);
	boolean final[MaxViewNum];
	int i,k,j,v,min,x;
	for(v=1;v<=N;v++)
	{
	final[v]=FALSE;
	d[v]=M.length[v0][v];
	if(d[v]<MaxRoad&&d[v]!=0)
	p[v]=v0;
	else
	p[v]=-1;
	}
	final[v0]=TRUE;
	d[v0]=0;
	for(i=2;i<=N;i++)
	{
		min=MaxRoad;
		for(k=1;k<=N;++k)
		if(!final[k]&&d[k]<min)
		{
			v=k;
			min=d[k];
		}
	
		if(min==MaxRoad)
		return;
		final[v]=TRUE;
		for(k=1;k<=N;++k)
		if(!final[k]&&(min+M.length[v][k]<d[k]))
		{
			d[k]=min+M.length[v][k];
			p[k]=v;
		}
	}
}

void printsyjd()
{
	int st[MaxViewNum],i,pre,top=-1;
	for(i=1;i<=N;i++)
	{
		printf("\nArrival Attraction %2d The total distance is %5d , The path passed through:",i,d[i]);
		st[++top]=i;
		pre=p[i];
		while(pre!=-1)
		{
			st[++top]=pre;
			pre=p[pre];
		}
	while(top>0)
	{
	printf("%d",st[top--]);
	if(top>0)
	printf("---");
	}
	}
	getch();
}

void dijkstra_ygjd()
{
	int v0;
	printf("Please enter the departure Attraction:");
	scanf("%d",&v0);
	boolean final[MaxViewNum];
	int i,k,j,v,min,x;
	for(v=1;v<=N;v++)
	{
	final[v]=FALSE;
	d[v]=M.length[v0][v];
	if(d[v]<MaxRoad&&d[v]!=0)
	p[v]=v0;
	else
	p[v]=-1;
	}
	final[v0]=TRUE;
	d[v0]=0;
	for(i=2;i<=N;i++)
	{
		min=MaxRoad;
		for(k=1;k<=N;++k)
		if(!final[k]&&d[k]<min)
		{
			v=k;
			min=d[k];
		}
	
		if(min==MaxRoad)
		return;
		final[v]=TRUE;
		for(k=1;k<=N;++k)
		if(!final[k]&&(min+M.length[v][k]<d[k]))
		{
			d[k]=min+M.length[v][k];
			p[k]=v;
		}
	}
}

void printygjd()
{
	int y;
	printf("\nPlease enter the arrival Attraction:");
	scanf("%d",&y);
	int st[MaxViewNum],i,pre,top=-1;
	for(i=1;i<=N;i++)
	{
		if(i==y) 
		printf("\nThe total distance is %5d , The path passed through:",d[i]);
		st[++top]=i;
		pre=p[i];
		while(pre!=-1)
		{
			st[++top]=pre;
			pre=p[pre];
		}
	while(top>0)
	{
	if(i==y)
	{
	printf("%d",st[top--]);
	if(top>0)
	printf("---");
	}
	else
	top--;
	}
	}
	getch();
}

void scdt()
{
	int i,j;
	char s[100];
	strcpy(s,"Map of Xijing University");
	initgraph(1200,800); 
	for(i=1;i<=N;i++)
	{
		setfillcolor(RGB(225,236,0));
		fillcircle(M.jd[i].x,M.jd[i].y,20);
		outtextxy(M.jd[i].x,M.jd[i].y,M.jd[i].name);
	}
	for(i=1;i<=N;i++)
		for(j=1;j<=N;j++)
		{
			if(M.length[i][j]>0&&M.length[i][j]<1000)
				line(M.jd[i].x,M.jd[i].y,M.jd[j].x,M.jd[j].y);
		}
	outtextxy(900,650,s);
	getch();
	closegraph();
}



main()
{
	init(); 
	int x;
	while(1)
	{
		printf("**********************************************************************\n");
		printf("*         =.=                                          =.=           *\n");
		printf("*    `                                                        `      *\n");
		printf("*     `           Master, welcome to Xijing~ Meow~           `       *\n");
		printf("*      `              ^-^                  ^-^              `        *\n");
		printf("*       `                       ^-^                        `         *\n");
		printf("**********************************************************************\n");
    	printf("\n                    Xijing Guide System(Enter 0 to exit the program):");
		printf("\n                     1. Output all Attraction and its Introduction");
		printf("\n                     2. Query a certain Attraction and its Introduction");
		printf("\n                     3. Add an Attraction");
		printf("\n                     4. Delete an Attraction");
		printf("\n                     5. Update an Attraction");
		printf("\n                     6. Add a road");
		printf("\n                     7. Remove a road");
		printf("\n                     8. Update a road");
		printf("\n                     9. Query the shortest path from an Attraction to all other Attraction");
		printf("\n                    10. Query the shortest path between two Attraction   ");
		printf("\n                    11. Output map                       Already Attraction:%d\n",N);
		printf("Please enter options:"); 
		scanf("%d",&x);
		if(x==0)
		break;
		else
			switch(x)
			{
				case 1:scsyjd();break;
				case 2:cxjd();break;
				case 3:zengj();break;
				case 4:scjd();break;
				case 5:gxjd();break;
				case 6:zengjl();break;
				case 7:scl();break;
				case 8:gxl();break;
				case 9:dijkstra_syjd();printsyjd();break;
				case 10:dijkstra_ygjd();printygjd();break;
				case 11:scdt();break;
			} 
			system("cls");
	}
}
```