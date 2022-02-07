### 题目

分子量（Molar Mass, ACM/ICPC Seoul 2007, UVa1586）
给出一种物质的分子式（不带括号），求分子量。本题中的分子式只包含4种原子，分别为C,H,O,N，原子量分别为12.01，1.008，16.00，14.01（单位：g/mol）。例如，C6H5OH的分子量为94.108g/mol。

Sample Input
4
C
C6H5OH
NH2CH2COOH
C12H22O11

Sample Output
12.010
94.108
75.070
342.296

### 代码

```c
#include <stdio.h>
#include <ctype.h>


int main()
{
    char s[50];
    int T;
    scanf("%d",&T);

    while(T--)
    {
        char *p = s;
        double ans = 0;
        scanf("%s",s);
        while(*(p+1)!='\0') p++;
        while(p>=s)
        {
            int n = 1;
            if(isdigit(*p))
            {
                n=*p-'0';
                p--;
                /*角标时两位数*/
                if(isdigit(*p))
                {
                    n += (*p-'0')*10;
                    p--;
                }
            }
            switch (*p)
            {
                case 'H': ans += 1.008 * n;break;
                case 'C': ans += 12.01 * n;break;
                case 'O': ans += 16.00 * n;break;
                case 'N': ans += 14.01 * n;break;
            }
            p--;
        }
        printf("%.3f%c",ans,(T? '\n':'\0'));
    }

    return 0;
}

```

