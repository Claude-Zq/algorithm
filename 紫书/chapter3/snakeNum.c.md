#蛇形填数#

时间：2022/1/23

```c
#include <stdio.h>
#define maxn 8
int a[maxn][maxn];

/*输出数组*/
void PrintArr(int a[][maxn],int m,int n)
{
    for (int i = 0;i < m;i++)
    {
        if (i) printf("\n"); /*除第一行都先换行*/
        for (int j = 0; j < n;j++)
        {

            printf("%-3d",a[i][j]);
        }
    }
}



int main()
{

    int n;
    scanf("%d",&n);
    /*给二维数组初始换*/
    for (int i = 0;i < maxn;i++)
    {
        for (int j = 0;j <maxn;j++)
        {
            if(j>=n||i>=n) a[i][j] = 1;
            else a[i][j] = 0;
        }
    }


    int j = n-1,i=0,count = 0;

    while(1)
    {
        /*下*/
        for(;i<=n-1&&a[i][j]==0;i++) a[i][j] = ++count;
        /*左*/
        for(--i,--j;j>=0&&a[i][j]==0;j--) a[i][j]=++count;
        /*上*/
        for(j++,i--;i>=0&&a[i][j]==0;i--) a[i][j]=++count;
        /*判断是否填完*/
        if (a[++i][++j]) break;
        /*右*/
        for (;a[i][j]==0;j++) a[i][j]=++count;
        ++i,--j;
    }

    /*打印结果*/
    PrintArr(a,n,n);

    return 0;
}

```

