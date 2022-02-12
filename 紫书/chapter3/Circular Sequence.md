## 题目

长度为n的环状串有n种表示法，分别为从某个位置开始顺时针得到。例如，下图的环状串有10种表示：CGAGTCAGCT，GAGTCAGCTC，AGTCAGCTCG等。在这些表示法中，字典序最小的称为"最小表示"。

输入一个长度为n（n≤100）的环状DNA串（只包含A、C、G、T这4种字符）的一种表示法，你的任务是输出该环状串的最小表示。例如，CTCC的最小表示是CCCT，CGAGTCAGCT的最小表示为AGCTCGAGTC。

## 输入案例：

2

CCTC

CGAGTCAGCT

## 输出案例：

CCCT

AGCTCGAGT



## 代码实现：

```c
#include <stdio.h>
#include <string.h>

/*比较两个字符指针所指字符串的字典序*/
//n字符数组的长度
// p < pmin : 1
// p 不小于pmin:0
int Func(char *p,char *pmin,int n)
{
    for (int i = 0;i < n;i++) if ((*p+i)!=(*pmin)) return *(p+i)<*(pmin+i);
    return 0; /*相等*/
}
int main()
{
     int T;
    scanf("%d",&T);

    while(T--)
    {
        char s[250];
        scanf("%s",s);
        int n = strlen(s);
        /*将s翻倍*/
        for (int i = 0;i < n;i++) s[i+n] = s[i];/*使用strcat()时，输入较长时会初现s溢出的bug*/ 
        char *pmin = s;/*指向最小的序列*/
        for (int i = 1;i < n;i++) if(Func(s+i,pmin,n)) pmin = s+i;
        /*输出答案*/
        for (int i = 0;i < n;i++) printf("%c",*(pmin+i));
        printf("\n");
    }
    return 0;
}

```





时间：2022、1、24

作者: 周青