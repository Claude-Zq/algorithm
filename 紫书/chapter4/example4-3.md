#### 题目

n(n<20)个人站成一圈，逆时针编号为1～n。有两个官员，A从1开始逆时针数，B从n开始顺时针数。在每一轮中，官员A数k个就停下来，官员B数m个就停下来（注意有可能两个官员停在同一个人上）。接下来被官员选中的人（1个或者2个）离开队伍。

输入n，k，m输出每轮里被选中的人的编号（如果有两个人，先输出被A选中的）。例如，n=10，k=4，m=3，输出为4 8, 9 5, 3 1, 2 6, 10, 7。注意：输出的每个数应当恰好占3列。

输入： 
10 4 3

输出： 
_ _ 4_ _ 8,_ _ 9_ _ 5,_ _ 3_ _ 1,_ _ 2_ _ 6,_ 10,_ _ 7



#### 代码

```c
#include <stdio.h>
#include<string.h>
#define maxn 20

int main()
{
    FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");
    
    int Q[maxn];
    int n,k,m;

    while(fscanf(fin,"%d%d%d",&n,&k,&m)==3&&n>0)
    {
        int left = n;
        memset(Q,-1,sizeof(Q)); /*-1表示人未被带走*/
        /*A、B在数组的位置*/
        int iA = n-1,iB = 0;

        while(left>0) /*每人时退出*/
        {
            //A移动
            for(int i = k;i>0;){iA = (iA+1)%n;if(Q[iA])i--;}
            //B移动
            for(int i = m;i>0;){if(--iB < 0) iB+=n; if(Q[iB])i--;}

            /*带走人*/
            if(iA == iB)
            {
                fprintf(fout,"%3d",iA+1);
                Q[iA] = 0;
                left--;
            }
            else
            {
                fprintf(fout,"%3d%3d",iA+1,iB+1);
                Q[iA] = Q[iB] = 0;
                left -= 2;
            }
            if(left) fprintf(fout,",");
        }
        fputc('\n',fout);
    }

    fclose(fin);
    fclose(fout);

    return 0;
}

```

