### 题目

把前n（n≤10000）个整数顺次写在一起：123456789101112…数一数0～9各出现多少次（输出10个整数，分别是0，1，…，9出现的次数）。

样例输入

2

3

13

样例输出

0 1 1 1 0 0 0 0 0 0

1 6 2 2 1 1 1 1 1 1



### 代码

```c
#include <stdio.h>

int main()
{
    int T;
    scanf("%d",&T);

    while(T--)
    {
        int ans[10] = {0};

        int n;
        scanf("%d",&n);
        for (int i = 1;i <= n;i++)
        {
            int j = i;
            while (j != 0){ans[j%10]++;j /= 10;}

        }

        for (int i = 0;i < 10;i++)
        {
            if(i) putchar(' ');
            printf("%d",ans[i]);
        }
        if(T) putchar('\n'); /*结尾无空行*/

    }

    return 0;
}

```
