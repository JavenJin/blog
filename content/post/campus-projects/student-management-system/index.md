---
title: Student management system (pure C implementation)
description: 学生管理系统（纯C语言实现）
date: '2018-12-20'
categories:
    - C (Programming Language)
tags:
    - C (Programming Language)
---
#### Student management system (pure C implementation)

```c
#include "stdio.h"
#include"string.h"
#include"stdlib.h" 

struct Student
{
     char ID[20];
     char Name[20];
     float Mark1;
     float Mark2;
     float Mark3;
     float Average;
};
 
struct Student students[1000];
int num=0;
 
float Avg(struct Student stu)
{
     return (stu.Mark1+stu.Mark2+stu.Mark3)/3;
}

int Student_SearchByIndex(char id[])
 
{
 
     int i;
     for (i=0;i<num;i++)
     {
         if (strcmp(students[i].ID,id)==0)
         {
              return i;
         }
     }
     return -1;
}

/*Returns the array subscript by Name*/
int Student_SearchByName(char Name[])
{
     int i;
     for (i=0;i<num;i++)
     {
         if (strcmp(students[i].Name,Name)==0)
         {
              return i;
         }
     }
     return -1;
}

/*Display a single student record*/ Student number
void Student_DisplaySingle(int index)
{
     printf("%10s%10s%8s%8s%8s%10s\n","Student number","Name","Higher Mathematics score","C Language score","Computers score","Average score");
     printf("-------------------------------------------------------------\n");
     printf("%10s%10s%8.2f%8.2f%8.2f%10.2f\n",students[index].ID,students[index].Name,students[index].Mark1,students[index].Mark2,students[index].Mark3,students[index].Average);
}

/*Insert student information*/ 
void Student_Insert()
{
     while(1)
     {
         printf("Please enter Student number:");
         scanf("%s",&students[num].ID);
         getchar();
         printf("Please enter Name:");
         scanf("%s",&students[num].Name);
         getchar();
         printf("Please enter Higher Mathematics score:");
         scanf("%f",&students[num].Mark1);
         getchar();
         printf("Please enter C Language score:");
         scanf("%f",&students[num].Mark2);
         getchar();
         printf("Please enter Computers score:");
         scanf("%f",&students[num].Mark3);
         getchar();
         students[num].Average=Avg(students[num]);
         num++;
         printf("Whether to continue?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*Modify student information*/
void Student_Modify()
{
     //float mark1,mark2,mark3;
     while(1)
     {
         char id[20];
         int index;
         printf("Please enter the student to be modified's Student number:");
         scanf("%s",&id);
         getchar();
         index=Student_SearchByIndex(id);
         if (index==-1)
         {
              printf("Students do not exist!\n");
         }
         else
         {
              printf("The student information you want to modify is:\n");
              Student_DisplaySingle(index);
              printf("-- Please enter a new value--\n");
              printf("Please enter Student number:");
              scanf("%s",&students[index].ID);
              getchar();
              printf("Please enter Name:");
              scanf("%s",&students[index].Name);
              getchar();
              printf("Please enter Higher Mathematics score:");
              scanf("%f",&students[index].Mark1);
              getchar();
              printf("Please enter C Language score:");
              scanf("%f",&students[index].Mark2);
              getchar();
              printf("Please enter Computers score:");
              scanf("%f",&students[index].Mark3);
              getchar();
              students[index].Average=Avg(students[index]);
         }
         printf("Whether to continue?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*Delete Student Information*/
void Student_Delete()
{
     int i;
     while(1)
     {
         char id[20];
         int index;
         printf("Please enter the student to be deleted's Student number:");
         scanf("%s",&id);
         getchar();
         index=Student_SearchByIndex(id);
         if (index==-1)
         {
              printf("Students do not exist!\n");
         }
         else
         {
              printf("The student information you want to delete is:\n");
              Student_DisplaySingle(index);
              printf("Is it really necessary to delete?(y/n)");
              if (getchar()=='y')
              {
                   for (i=index;i<num-1;i++)
                   {
                       students[i]=students[i+1];//Move all the objects behind you forward
                   }
                   num--;
              }
              getchar();
         }
         printf("Whether to continue?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*Search by Name*/
void Student_Select()
{
     while(1)
     {
         char Name[20];
         int index;
         printf("Please enter the student's Name:");
         scanf("%s",&Name);
         getchar();
         index=Student_SearchByName(Name);
         if (index==-1)
         {
              printf("Students do not exist!\n");
         }
         else
         {
              printf("The student information you are looking for is:\n");
              Student_DisplaySingle(index);
         }
         printf("Whether to continue?(y/n)");
         if (getchar()=='n')
         {
              break;
         }
     }
}
 
/*Sort by average*/
void Student_SortByAverage()
{
     int i,j;
     struct Student tmp;
     for (i=0;i<num;i++)
     {
         for (j=1;j<num-i;j++)
         {
              if (students[j-1].Average<students[j].Average)
              {
                   tmp=students[j-1];
                   students[j-1]=students[j];
                   students[j]=tmp;
              }
         }
     }
}
 
/*Show student information*/
void Student_Display()
{
     int i;
     printf("%10s%10s%8s%8s%8s%10s\n","Student number","Name","Higher Mathematics score","C Language score","Computers score","Average score");
     printf("-------------------------------------------------------------\n");
     for (i=0;i<num;i++)
     {
         printf("%10s%10s%8.2f%8.2f%8.2f%10.2f\n",students[i].ID,students[i].Name,students[i].Mark1,students[i].Mark2,students[i].Mark3,students[i].Average);
     }
}
 
/*Read student information out of the file*/
void IO_ReadInfo()
{
     FILE *fp;
     int i;
     if ((fp=fopen("Database.txt","rb"))==NULL)
     {
         printf("Cannot open file!\n");
         return;
     }
     if (fread(&num,sizeof(int),1,fp)!=1)
     {
         num=-1;
     }
     else
     {
         for(i=0;i<num;i++)
         {
              fread(&students[i],sizeof(struct Student),1,fp);
         }
     }
     fclose(fp);
}
 
/*Writing student information to a file*/
void IO_WriteInfo()
{
     FILE *fp;
     int i;
     if ((fp=fopen("Database.txt","wb"))==NULL)
     {
         printf("Cannot open file!\n");
         return;
     }
     if (fwrite(&num,sizeof(int),1,fp)!=1)
     {
         printf("Write to file error!\n");
     }
     for (i=0;i<num;i++)
     {
         if (fwrite(&students[i],sizeof(struct Student),1,fp)!=1)
         {
              printf("Write to file error!\n");
         }
     }    
     fclose(fp);
}
 
/*Main Program*/
void main()
{
     int choice;
     IO_ReadInfo();
     while(1)
     {
         /*Main Menu*/
         printf("\n------ Student Management System------\n");
         printf("1. Adding student records\n");
         printf("2. Modify student records\n");
         printf("3. Delete student records\n");
         printf("4. Search Student Records by Name\n");
         printf("5. Sorted by average score\n");
         printf("6. Exit\n");
         printf("Please select(1-6):");
         scanf("%d",&choice);
         getchar();
         switch(choice)
         {
         case 1:
              Student_Insert();
              break;
         case 2:
              Student_Modify();
              break;
         case 3:
              Student_Delete();
              break;
         case 4:
              Student_Select();
              break;
         case 5:
              Student_SortByAverage();
              Student_Display();
              break;
         case 6:
              exit(0);
              break;
         }
         IO_WriteInfo();
     }
}
```