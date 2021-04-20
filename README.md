# 2021-04-20
练习数组、指针、字符串！

1、从键盘输入一行字符（最长不超过80字符），
用函数编程统计其中单词（以空格作为间隔符的字符串）的个数。
例如How  are  you中单词个数为3。
要求：
(1)按如下函数原型进行编程：
	 int CountWords(char str[])
(2)在主函数中：
     输入一行字符;
     然后调用函数CountWords计算单词的个数;
     最后打印计算结果。
     **输入提示信息为："Input a string:\n"
     **输出格式为:"Number of words=%d\n"
    
我的答案：
#include<stdio.h>

int CountWords(char str[]);
 
int main(int argc,char const *argv[])
{
	char s[80];
	int count = 0;
	
	printf("Input a string:\n");
	gets(s);

	count = CountWords(s);
	printf("Number of words=%d\n",count);
	 
    return 0; 
}

int CountWords(char str[])
{
	int cnt;
	int i,j = 0;
	if (str[0] == ' ')//以空格开头不计入单词数 
		cnt = -1;
	else
		cnt = 0;
	for (i=0 ; str[i]!='\0' ; )
	{
		while (str[j] != ' ' && str[j] != '\0')
		{
			j++;
			i++;
		}
		while (str[j] == ' ')//跳过单词之间的空格，str[j]=='\0'时也不会执行此句 
		{
			i++;
			j++;
		}
		cnt++;
	}
	return cnt;
}

标准答案：
#include <stdio.h>
int CountWords(char str[]);
void main()
{                        
    char  str[80];
    int num;
        printf("Input a string:\n");
    gets(str);//2
    num=CountWords(str);//2
    printf("Number of words=%d\n", num);//2
}                        
int CountWords(char str[])
{                        
    int    i, num;
    if(str[0]!=' ') //2
        num=1;//1
    else
        num=0;//1
    for (i=1; str[i]!='\0'; i++)//4
    {                        
        if (str[i]!=' ' && str[i-1] == ' ') //4
        {                        
            num++;//1
        }
    }
    return num;//1
}

对完标准答案改进我的答案：
#include<stdio.h>

int CountWords(char str[]);
 
int main(int argc,char const *argv[])
{
	char s[80];
	int count = 0;
	
	printf("Input a string:\n");
	gets(s);

	count = CountWords(s);
	printf("Number of words=%d\n",count);
	 
    return 0; 
}

int CountWords(char str[])
{
	int cnt;
	int i; 
	if (str[0] == ' ')//以空格开头不计入单词数 
		cnt = -1;
	else
		cnt = 0;
	for (i=0 ; str[i]!='\0' ; )
	{
		while (str[i] != ' ' && str[i] != '\0')
		{
			i++;
		}
		while (str[i] == ' ')//跳过单词之间的空格，str[i]=='\0'时也不会执行此句 
		{
			i++;
		}
		cnt++;
	}
	return cnt;
}
总结：不需要使用双重循环！向函数传递数组之后，只能用形参里的数组名来表示数组。
但本质上处理的还是原数组（传入的）。

2、输入不超过20个非负整数（输入每个整数后按回车，以-1结束且不计入整数个数），用一维数组作函数参数编程实现如下功能：
（1）录入每个整数，函数原型：unsigned short ReadNumber(int num[])，num存储输入的整数，返回值为输入整数的个数；

（2）按由高到低的顺序排序，函数原型：void SortNumberDescending(int num[], unsigned short n)，n为整数个数；

（3）对这些整数求和及平均值，函数原型：void SummingAveraging(int num[], unsigned short n, int *pSum, float *pAver)，pSum指向和变量，pAver指向平均值变量；

（4）输出这些整数，函数原型：void  PrintNumber(int num[], unsigned short n) 。

主函数中按以下示例形式提示输入、调用函数（1）、调用函数（2）、提示输出、调用函数（4）、调用函数（3）、输出整数和及平均值。
Input Numbers:
87
100
...
23
-1

Sort in descending order:
100
...
23

Sum=474,Aver=59.25

输入格式：
"Input Numbers:\n"
"%d"
输出格式：
"\nSort in descending order:\n"
"\nSum=%d,Aver=%.2f\n"
"%d\n"

我的答案：
#include<stdio.h>

unsigned short ReadNumber(int num[]);
void SortNumberDescending(int num[], unsigned short n);
void SummingAveraging(int num[], unsigned short n, int *pSum, float *pAver);
void PrintNumber(int num[], unsigned short n);

int main(int argc,char const *argv[])
{
	unsigned int a[20];
	unsigned short n;
	int sum = 0;
	float aver = 0.0;
	int *pSum = &sum;
	float *pAver = &aver;
	
	printf("Input Numbers:\n");
	n = ReadNumber(a);
	
	SortNumberDescending(a,n);
	printf("\nSort in descending order:\n");
	PrintNumber(a,n);
	
	SummingAveraging(a, n, pSum, pAver);
	printf("\nSum=%d,Aver=%.2f\n",sum,aver);
    
	return 0; 
}
/*函数功能：录入非负整数并返回整数个数*/ 
unsigned short ReadNumber(int num[])
{
	int i = 0;
	unsigned short cnt = 0;
	scanf("%d",&num[i]);
	while (num[i] != -1)
	{
		cnt++;
		i++;
		scanf("%d",&num[i]);
	}
	return cnt;
}
/*函数功能：冒泡法降序排序*/ 
void SortNumberDescending(int num[], unsigned short n)
{
	int i, j, temp;
	for (i=0 ; i<n-1 ; i++)
	{
		for (j=0 ; j<n-1-i ; j++)
		{
			if (num[j] < num[j+1])
			{
				temp = num[j];
				num[j] = num[j+1];
				num[j+1] = temp;
			}
		}
	}
}
/*函数功能：计算总和及平均值*/ 
void SummingAveraging(int num[], unsigned short n, int *pSum, float *pAver)
{
	int i;
	for (i=0 ; i<n ; i++)
	{
		*pSum += num[i];
	}
	*pAver = *pSum / (float)n;
}
/*函数功能：输出所有整数*/ 
void PrintNumber(int num[], unsigned short n)
{
	int i;
	for (i=0 ; i<n ; i++)
	{
		printf("%d\n",num[i]);
	}
}
总结：没啥好总结的😂，一个一个函数写就完事了，费点时间而已，涉及知识面很广。
