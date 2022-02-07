# 猜数字

## 题目

实现一个经典"猜数字"游戏。给定答案序列和用户猜的序列，统计有多少数字位置正确 （A），有多少数字在两个序列都出现过但位置不对（B）。
输入包含多组数据。每组输入第一行为序列长度n，第二行是答案序列，接下来是若干 猜测序列。猜测序列全0时该组数据结束。n=0时输入结束。

## 样例输入

4
1 3 5 5
1 1 2 3
4 3 3 5
6 5 5 1
6 1 3 5
1 3 5 5
0 0 0 0
10
1 2 2 2 4 5 6 6 6 9
1 2 3 4 5 6 7 8 9 1
1 1 2 2 3 3 4 4 5 5
1 2 1 3 1 5 1 6 1 9
1 2 2 5 5 5 6 6 6 7
0 0 0 0 0 0 0 0 0 0
0

## 样例输出

Game 1:
      (1,1)
      (2,0)
      (1,2)
      (1,2)
      (4,0)
Game 2:
      (2,4)
      (3,2)
      (5,0)
      (7,0)

## 解题思路

易：直接统计可得A

难：对1-9的每个数字，统计其答案序列和猜测序列出现的次数c1和c2,min(c1,c2)就是该数字在两序列错开时对B的贡献。最后将1-9的min(c1,c2)求和后减去A就是B

## 代码

需要在代码的目录里面创建一个“input.txt"文件用来存放输入，输出结果会放在“output.txt"文件中

```c
#include <stdio.h>
#define maxn 1010

/*判断数组全部元素是否为零*/
int AllZero(int a[],int n)
{
    for (int i = 0; i < n;i++)
    {
        if(a[i]!=0) return 0;
    }
    return 1;
}

/*求A*/
int ComputA(int a[],int b[],int n)
{
    int ret = 0;
    for (int i = 0;i < n;i++)
    {
        if (a[i]==b[i]) ret++;
    }
    return ret;
}

/*求B*/
int ComputB(int a[],int b[],int n)
{
    int B = 0;
    for (int i = 1;i <= 9;i++)
    {
        int c1=0,c2=0;
        for (int j = 0;j < n;j++)
        {
            if (a[j] == i) c1++;
            if (b[j] == i) c2++;
        }
        B += (c1 < c2? c1:c2);
    }

    return B-ComputA(a,b,n);
}

int main()
{   FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");
    
    int a[maxn],b[maxn];
    int n,kGame = 0;

    while(fscanf(fin,"%d",&n)!=EOF)
    {
        if (n==0) break;/*n为结束*/

        for (int i = 0;i < n;i++) fscanf(fin,"%d",a+i);
        if(kGame) fprintf(fout,"\n");
        fprintf(fout,"Game %d:",++kGame);

        do{
            for (int i = 0;i <n;i++) fscanf(fin,"%d",b+i);
            if(AllZero(b,n)) break;/*b全为零，结束*/

            int A = ComputA(a,b,n);
            int B = ComputB(a,b,n);

            fprintf(fout,"\n      (%d,%d)",A,B);
        }while(1);
    return 0;
}

```

