# homework
#include"stdio.h"  //标准的输入输出函数文件头部说明 
#include"math.h"    // 数学函数头部说明 
#include"string.h" 
#include"stdlib.h" //通过该函数头部里的函数，改变控制台的背景和颜色 
#include"windows.h" //头文件声明，下文用到了改变控制台的宽度和高度 
#define M 100   //宏定义说明 
struct student{ //结构体定义并声明 
 char name[25];  //姓名 
 char num[25];  //学号 
 char sex[25];//性别 
 int old;  //年龄 
 int math,yy,yw; //数学、英语、语文 
 int all;};  //总分 
//****************************************函数的声明******************************************** 
void input(struct student stu[M]);  //输入函数 
void output(struct student stu[M]);  //各类用户自定义函数的声明 
void lookfor(struct student stu[M]); //查询函数 
void modify(struct student stu[M]);  //修改函数  
void delete_student(struct student stu[M]); //删除函数 
void fileread(struct student stu[M]); 
void filewrite(struct student stu[M]); 
void yanshi(char *p);  //延时函数说明 
int FileWrite(struct student stu[M]);
int FileRead(struct student stu[M]);
//********************************************************************************************** 
int count=0; 
struct student t; 
int main() 
{ 
 int choice,sum; 
 struct student stu[M];   
 system("mode con:cols=400 lines=30000");  //调节控制台的宽度和高度 
  system("color 0b");  //调节控制台的背景和字体颜色 
point1: 
 sum=0; 
 yanshi("\t\t\t\t\t\t\t\t\3\3\3\3\3\3\3\3\3\3\3\3\3欢迎你使用学生信息管理系统\3\3\3\3\3\3\3\3\3\3\n"); 
 do { 
	printf("**********欢迎使用学生信息管理系统（当前共有0名学生)*********\n");
	printf("*                                                           *\n");
	printf("*              --------------------------------             *\n");
	printf("*              |    Powered By YongFU Lee     |             *\n");
	printf("*              --------------------------------             *\n");
	printf("*                                                           *\n");
	printf("*              1）添加学生信息                              *\n");
	printf("*              2）显示所有学生信息及统计信息                *\n");
	printf("*              3）查询学生信息                              *\n");
	printf("*              4）修改学生信息 （根据学号）                 *\n");
	printf("*              5）删除学生信息 （根据学号）                 *\n");
	printf("*              0）退出软件                                  *\n");
	printf("*                                                           *\n");
	printf("*************************************************************\n");
 printf("请输入你的选择\n"); 
 scanf("%d",&choice); 
 fflush(stdin);  //清除输入缓冲区 
 if (choice>5||choice<=0) 
 { 
 sum++; 
 if (sum>=5) 
 { 
 printf("输入错误次数过多,程序将重新开始\n"); 
 system("pause");  //程序暂停 
 system("cls"); //清屏语句 
 goto point1; 
 } 
 } 
 switch (choice)  //根据选择，调用不同的函数来完成不同的任务 
 { 
 case 1:input(stu);break;   
 case 2:output(stu);break; 
 case 3:lookfor(stu);break; 
 case 4:modify(stu);break; 
 case 5:delete_student(stu);break; 
 case 0:printf("感谢你使用学生信息管理系统,请关掉程序!!!\n");system("pause");break; 
 default:printf("无效的选择!!!请重新输入!!!\n");break; 
 } 
 }while (choice!=0); 
 printf("the program is over!!!\n"); 
  return 0; 
} 
void input(struct student stu[M])  //自定义输入函数 
{ 
 int len,size; 
 system("cls"); 
 printf("请添加要输入学生的信息\n"); 
 do 
 { 
 	printf("请输入由2位数字组成的学生学号\n"); //do-while循环应用，提示输入位数为一确定数 
	scanf("%s",&stu[count].num); 
 	len=strlen(stu[count].num); 
 }while(len!=2); 
 do{
 	printf("请输入同学的姓名\n"); 
	 scanf("%s",stu[count].name); 
 	printf("请输入数学成绩\n"); 
 	scanf("%d",&stu[count].math); 
 	if(stu[count].math>150)
 		printf("成绩的区间为0-150\n"); 
	 printf("请输入英语成绩\n");
 	scanf("%d",&stu[count].yy); 
  	if(stu[count].yy>150)
 		printf("成绩的区间为0-150\n"); 
	 printf("请输入语文成绩\n");
 	scanf("%d",&stu[count].yw); 
  	if(stu[count].yw>150)
 		printf("成绩的区间为0-150\n"); 
	} while(stu[count].math>100||stu[count].yy>100||stu[count].yw>100);  
 	stu[count].all=stu[count].math+stu[count].yy+stu[count].yw;  //求出总分 
	printf("请输入性别\n");
	 scanf("%s",stu[count].sex);
 count++; 
} 

void output(struct student stu[M])  //自定义输出函数 
{ 
 int j; 
 system("cls"); 
 if (count==0) 
	{ 
		 printf("当前已存学生信息为0个\n"); 
		 return; 
 	} 
 for (j=0;j<count;j++) 
 { 
 	 printf("-------------------------------------------------------\n");
	 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
	 printf("-------------------------------------------------------\n");
 	for (j=0;j<count;j++)
	{ 						 

	 printf("%s    |",stu[j].num); 
	 printf("%s  |",stu[j].name); 
	 printf("%s    |",stu[j].sex);
	 printf("%d    |",stu[j].old);
	 printf("%d    |",stu[j].math); 
	 printf("%d    |",stu[j].yy); 
	 printf("%d    |",stu[j].yw); 
 	 printf("%d    |\n",stu[j].all); 
 	 printf("-----------------------------------------------\n");
 	} 
 } 
} 
void lookfor(struct student stu[M])     //自定义查询学生信息函数 
{ 
 int j,a,m,n=0; 
 char name[25];
 char xh[25]; 
 system("cls"); 
 if (count==0) 
 { 
 	printf("当前已存学生信息为0个,无法查询!!!\n"); 
 	return; 
 } 
 else
 { 
    printf("*************查询学生信息（当前共有0名学生)******************\n");
	printf("*                                                           *\n");
	printf("*              1）根据学号查询                              *\n");
	printf("*              2）根据姓名查询                              *\n");
	printf("*              3）根据数学成绩查询                          *\n");
	printf("*              4）根据英语成绩查询                          *\n");
	printf("*              5）根据语文成绩查询                          *\n");
	printf("*              6）根据总成绩查询                            *\n");
	printf("*              0）返回主菜单                                *\n");
	printf("*                                                           *\n");
	printf("*************************************************************\n"); 
 	scanf("%d",&a); 
 	fflush(stdin); 
 	if(a==1)
 	{
 		printf("请输入学号\n"); 
		 scanf("%s",&xh); 
		 for (j=0;j<count;j++) 
 		{ 
 			if (strcmp(stu[j].num,xh)==0)  // 按学号查询：通过字符函数对已存入的学生信息进行比较,找出要查看的学生 
			 { 
 			 printf("-------------------------------------------------------\n");
			 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
			 printf("-------------------------------------------------------\n");
			 printf("%s    |",stu[j].num); 
			 printf("%s  |",stu[j].name); 
			 printf("%s    |",stu[j].sex);
			 printf("%d    |",stu[j].old);
			 printf("%d    |",stu[j].math); 
			 printf("%d    |",stu[j].yy); 
			 printf("%d    |",stu[j].yw); 
 			 printf("%d    |\n",stu[j].all); 
 			 printf("-----------------------------------------------\n");
 			} 
 			if (strcmp(stu[j].num,xh)!=0)
			 printf("很抱歉,没有你所需要的学生信息\n"); 
 		} 
	}
	if(a==2)//按姓名查询成绩
	{
		printf("输入要查询学生的姓名：");
        scanf("%s",name);
		for(int i=0;i<count;i++)
		{
			if(strcmp(stu[i].name,name)==0)
			 { 
 				 printf("-------------------------------------------------------\n");
				 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
				 printf("-------------------------------------------------------\n");
				 printf("%s    |",stu[i].num); 
				 printf("%s  |",stu[i].name); 
				 printf("%s    |",stu[i].sex);
				 printf("%d    |",stu[i].old);
				 printf("%d    |",stu[i].math); 
				 printf("%d    |",stu[i].yy); 
				 printf("%d    |",stu[i].yw); 
 				 printf("%d    |\n",stu[i].all); 
 				 printf("-----------------------------------------------\n");
 			} 
 			if(strcmp(stu[i].name,name)!=0)
 			printf("没有查询到该学生，请重新输入学生姓名"); 
		}
	} 
	if(a==3)//按输入的数学成绩范围来查询学生的成绩
	{
		printf("请输入要查询的成绩范围\n");
		scanf("%d",&m);//成绩下限 
		scanf("%d",&n);//成绩上限
		for(int i=0;i<count;i++)
		{
			if(stu[i].math>m&&stu[i].math<n)
			{
				printf("-------------------------------------------------------\n");
				 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
				 printf("-------------------------------------------------------\n");
				 printf("%s    |",stu[i].num); 
				 printf("%s  |",stu[i].name); 
				 printf("%s    |",stu[i].sex);
				 printf("%d    |",stu[i].old);
				 printf("%d    |",stu[i].math); 
				 printf("%d    |",stu[i].yy); 
				 printf("%d    |",stu[i].yw); 
 				 printf("%d    |\n",stu[i].all); 
 				 printf("-----------------------------------------------\n");
			}
		 } 
	} 
	if(a==4)//按输入的英语成绩范围来查询学生的成绩
	{
		printf("请输入要查询的成绩范围\n");
		scanf("%d",&m);//成绩下限 
		scanf("%d",&n);//成绩上限
		for(int i=0;i<count;i++)
		{
			if(stu[i].yy>m&&stu[i].yy<n)
			{
				printf("-------------------------------------------------------\n");
				 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
				 printf("-------------------------------------------------------\n");
				 printf("%s    |",stu[i].num); 
				 printf("%s  |",stu[i].name); 
				 printf("%s    |",stu[i].sex);
				 printf("%d    |",stu[i].old);
				 printf("%d    |",stu[i].math); 
				 printf("%d    |",stu[i].yy); 
				 printf("%d    |",stu[i].yw); 
 				 printf("%d    |\n",stu[i].all); 
 				 printf("-----------------------------------------------\n");
			}
		 } 
	} 
 	if(a==5)//按输入的语文成绩范围来查询学生的成绩
	{
		printf("请输入要查询的成绩范围\n");
		scanf("%d",&m);//成绩下限 
		scanf("%d",&n);//成绩上限
		for(int i=0;i<count;i++)
		{
			if(stu[i].yw>m&&stu[i].yw<n)
			{
				printf("-------------------------------------------------------\n");
				 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
				 printf("-------------------------------------------------------\n");
				 printf("%s    |",stu[i].num); 
				 printf("%s  |",stu[i].name); 
				 printf("%s    |",stu[i].sex);
				 printf("%d    |",stu[i].old);
				 printf("%d    |",stu[i].math); 
				 printf("%d    |",stu[i].yy); 
				 printf("%d    |",stu[i].yw); 
 				 printf("%d    |\n",stu[i].all); 
 				 printf("-----------------------------------------------\n");
			}
		 } 
	} 
	if(a==6)//按输入的总分成绩范围来查询学生的成绩
	{
		printf("请输入要查询的成绩范围\n");
		scanf("%d",&m);//成绩下限 
		scanf("%d",&n);//成绩上限
		for(int i=0;i<count;i++)
		{
			if(stu[i].all>m&&stu[i].all<n)
			{
				printf("-------------------------------------------------------\n");
				 printf("学号 | 姓名 | 性别 | 年龄 | 数学 | 英语 | 语文 | 总分 |\n"); 
				 printf("-------------------------------------------------------\n");
				 printf("%s    |",stu[i].num); 
				 printf("%s  |",stu[i].name); 
				 printf("%s    |",stu[i].sex);
				 printf("%d    |",stu[i].old);
				 printf("%d    |",stu[i].math); 
				 printf("%d    |",stu[i].yy); 
				 printf("%d    |",stu[i].yw); 
 				 printf("%d    |\n",stu[i].all); 
 				 printf("-----------------------------------------------\n");
			}
		 } 
	} 
	if(a==0)
	return;
 } 
}  

void modify(struct student stu[M]) //自定义修改函数 
{ 
 int j,flag=0,course; 
 char xh[25]; 
 system("cls"); 
 if (count==0) 
 { 
 printf("当前已存学生信息为0个,无法修改!!!\n"); 
 return; 
 } 
 else
 { 
 printf("请输入你想要修改的同学学号\n"); 
 scanf("%s",&xh); 
 fflush(stdin); 
 for (j=0;j<count;j++) 
 if (strcmp(stu[j].num,xh)==0)  //同上 
 { 
 printf("你确定要修改学生的信息吗???如果不确定的话,请关掉本程序吧!!!\n"); 
 printf("选择课程: 1、数学 2、英语 3、语文\n"); 
 scanf("%d",&course); 
 printf("请输入你想要修改后的学生成绩\n"); 
 switch(course) 
 { 
 case 1:scanf("%d",&stu[j].math);break; 
 case 2:scanf("%d",&stu[j].yy);break;  //switch控制语句 
 case 3:scanf("%d",&stu[j].yw);break; 
 default:printf("无效的选择!!!请重新输入!!!\n");break; 
 } 
 } 
 } 
} 
void delete_student(struct student stu[M])  //自定义删除函数 
{ 
 int choice; 
 system("cls"); 
 if (count==0) 
 { 
	 printf("当前已存学生信息为0个,无法删除!!!\n"); 
	 return; 
 } 
 else
 { 
	int j,index=0,k=count; 
 	char xh[25]; 
	 system("cls"); 
 	printf("请输入你想要删除的同学学号\n"); 
 	scanf("%s",xh); 
	 fflush(stdin); 
 	for (j=0;j<count;j++) 
 	{ 
 		if (strcmp(stu[j].num,xh)==0) 
		{  
 			for(j=index;j<count;j++) 
			{
 				stu[j]=stu[j+1]; 
 				count--; 
				if (count<k) 
				printf("你已经删除成功\n"); 
			}
 		} 
 	}
 	index++;
 	if (j==count) 
	 printf("抱歉!!!没有你所需要删除的学生信息!*_*!\n");
 } 
 	
 } 



void yanshi(char *p)    //延时函数的定义 
{ 
 while (1) 
 { 
 if (*p!=0) 
 printf("%c",*p++); 
 else
 break; 
 Sleep(100);    //延时控制间断语句 
 } 
} 
void filewrite(struct student stu[M])     //写入文件函数定义 
{ 
 int j=0; 
 char c; 
 FILE *fp; 
 fflush(stdin); 
 	if((fp=fopen("data","wb"))==NULL) 
 	{ 
 	 printf("文件打开错误,程序无法进行\n"); 
	  exit(0); 
 	} 
 	for(j=0;j<count;j++) 
  	{
	  fwrite(&stu[j],sizeof(struct student),1,fp); 
 	} 
 	fclose(fp); 
 	if(count==0) 
 	 printf("没有文件，无法保存\n"); 
 	else
 	printf("数据存储完毕\n"); 
 	system("pause"); 
} 
void fileread(struct student stu[M])     //读取文件信息函数定义 
{ 
 int j=0; 
 char c; 
 FILE *fp; 
 if((fp=fopen("d:\\stu.dat","rb"))==NULL) 
 { 
  printf("文件打开错误,程序无法进行\n"); 
  exit(0); 
 } 
 fread(&stu[j],sizeof(struct student),1,fp); 
 count=0; 
 count++; 
 j++; 
 while(fread(&stu[j],sizeof(struct student),1,fp)) 
 { 
  j++; 
  count++; 
 } 
 fclose(fp); 
 printf("数据读取完毕!!!\n"); 
 system("pause"); 
 }