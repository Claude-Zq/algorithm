### 题目

题目：输入一个 r 行 c 列的网格，黑格用“*”表示，每个白格都填有一个字母。如果一个白格的左边相邻位置或者上面相邻位置没有白格（可能是黑格，也可能出了网格边界），则称这个白格是一个起始格。
首先把所有起始格按照从上到下、从左到右的顺序编号为 1,2,3,… ,如图所示。
接下来要找出所有的横向单词（Across）。这些单词必须从一个起始格开始，向右延伸到一个黑格的左边或者整个网格的最右列。
最后找出所有的竖向单词（Down）。这些单词必须从一个起始格开始，向下延伸到一个黑格的上边或者整个网格的最下行。

```c
Sample Input
2 2
AT
*O
6 7
AIM*DEN
*ME*ONE
UPON*TO
SO*ERIN
*SA*OR*
IES*DEA
0

Sample Output
puzzle #1:
Across
1.AT
3.O
Down
1.A
2.TO
puzzle #2:
Across
1.AIM
4.DEN
7.ME
8.ONE
9.UPON
11.TO
12.SO
13.ERIN
15.SA
17.OR
18.IES
19.DEA
Down
1.A
2.IMPOSE
3.MEO
4.DO
5.ENTIRE
6.NEON
9.US
10.NE
14.ROD
16.AS
18.I
20.A

```





```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");

    int r,c,kcase = 0;
    while(fscanf(fin,"%d%d",&r,&c)==2)
    {
        if(r==0&&c==0) break;
        /*在堆区创建一个二维字符数组*/
        char** S = (char**)malloc(r*sizeof(char*));
        for (int i = 0;i < r;i++)
        {
            S[i] = (char *) malloc((c+2)*sizeof(char));
        }
         /*在堆区创建一个二维整形数组*/
        int** N = (int**)malloc(r*sizeof(int*));
        for (int i = 0;i < r;i++)
        {
            N[i] = (int*) malloc((c)*sizeof(int));
        }

        /*输入字符格子*/
        fgetc(fin); /*消掉回车*/
        for (int i = 0;i<r;i++) fgets(S[i],c+2,fin); /*必须保证输入样例每行最后没有空格*/


        /*将字符格子转为数字格子*/
        int num = 0;
        for(int i = 0;i <r;i++)
        {
            for (int j = 0;j < c;j++)
            {
                if(S[i][j] == '*') N[i][j] = 0; /*黑格子*/
                else
                {
                   if (!i||!j||S[i][j-1]=='*'||S[i-1][j]=='*') N[i][j] =++num;/*起始白格*/                    					 else N[i][j] = -1; /*普通白格子*/
                }
            }
        }

        fprintf(fout,"puzzle #%d:\n",++kcase);

        //打印横向单词
        fprintf(fout,"Across\n");
        for (int i = 0;i < r;i++)
        {
            for (int j = 0; j < c;j++)
            {
                if(N[i][j])
                {
                    fprintf(fout,"%d.",N[i][j]);
                    while(j<c&&N[i][j]) fprintf(fout,"%c",S[i][j++]);
                    fprintf(fout,"\n");
                }
            }
        }

        //打印纵向单词
        fprintf(fout,"Down\n");
        for (int i =0;i < r;i++)
            for (int j = 0;j < c;j++)
                if(N[i][j])
                {
                    fprintf(fout,"%d.",N[i][j]);
                    int k = i;
                    while(k<r&&N[k][j]){fprintf(fout,"%c",S[k][j]);N[k++][j]=0;}
                    fprintf(fout,"\n");
                }


        /*释放字符数组*/
        for (int i = 0;i < r;i++)
        {
            free(S[i]);
        }
        free(S);
         /*释放整形数组*/
        for (int i = 0;i < r;i++)
        {
            free(N[i]);
        }
        free(N);
    }

    fclose(fin);
    fclose(fout);
    return 0;
}



```

