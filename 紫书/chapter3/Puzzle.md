### 题目

一个5*5的网格中恰好有一个格子是空的，其他格子各有一个字母，四条指令A,B,L,R分别表示将空格上、下、左、右移动。输入初始网格和一串指令（以0结束），输出执行操作后的网格。越界则输出“This puzzle has no final configuration.”。



### 代码

```d
#include <stdio.h>
#include <string.h>

/*找到谜题的空格*/
void FindSpace(int *i,int *j,char s[][7])
{
    for (*i = 0;*i < 5;(*i)++)
        for (*j = 0; *j < 5;(*j)++) if(s[*i][*j] == ' ' ||s[*i][*j]=='\n') return;
}

/*判断对s[][]的位置ij空格的操作op是否合法*/
//若合法：完成操作并更新i,j
//若不合法：返回零
int Operate(char s[][7],int *i,int *j,char op)
{
    switch (op)
    {
        case 'A':
            {
                if(*i==0) return 0;
                s[*i][*j] = s[(*i)-1][*j];
                s[(*i)-1][*j] = ' ';
                (*i)--;/*更新空格位置*/
                break;
            }
        case 'B':
            {
                if(*i==4) return 0;
                s[*i][*j] = s[(*i)+1][*j];
                s[(*i)+1][*j] = ' ';
                (*i)++;/*更新空格位置*/
                break;
            }
        case 'L':
            {
                if(*j==0) return 0;
                s[*i][*j] = s[*i][(*j)-1];
                s[*i][(*j)-1] = ' ';
                (*j)--;/*更新空格位置*/
                break;
            }
        case 'R':
            {
                if(*j==4) return 0;
                s[*i][*j] = s[*i][(*j)+1];
                s[*i][(*j)+1] = ' ';
                (*j)++;/*更新空格位置*/
                break;
            }

        default: return 0;
    }
    /*成功操作*/
   return 1;
}

int main()
{
   	FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");
    char s[5][7];


    //录入谜题
    for (int i = 0;i<5;i++)
    {
        fgets(s[i],7,fin);
        fgetc(fin); /*后面还有回车,需要读走*/
    }

    //输入指令
    char op[50];
    fscanf(fin,"%s",op);

     //找到空格
    int ispace,jspace;
    FindSpace(&ispace,&jspace,s);

    int ok = 1;/*是否有结果*/
    for (int i = 0;op[i] != '0'&&op[i]!='\0';i++) /*遇到0或者空字符结束*/
        if (!Operate(s,&ispace,&jspace,op[i])){ok = 0;break;}

    //打印结果
    fputc('\n',fout);
    if(ok) for (int i = 0;i<5;i++) fprintf(fout,"%s",s[i]);
    else fprintf(fout,"This puzzle has no final configuration\n");

    fclose(fin);
    fclose(fout);
    return 0;
}

```

## 