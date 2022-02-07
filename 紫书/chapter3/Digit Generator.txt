# 生成元

## 题目：

如果x加上x的各个数字之和得到y，就说x是y的生成元。给出n（1≤n≤100000），求最小

生成元。无解输出0。例如，n=216，121，2005时的解分别为198，0，1979。



## 方法一：枚举法

效率不高

```c
#include <stdio.h>

int main()
{
    int n;
    char s[100];
    scanf("%d",&n);


    for (int i = 0;i < n;i++)
    {
        int sum = i;
        sprintf(s,"%d",i);
        for (int j = 0;s[j]!='\0';j++) sum += (s[j]-'0');
        if(sum == n) {printf("%d\n",i); return;}
    }
    printf("0\n");
    return 0;
}
```



## 方法二：

先一次性枚举所有数的小生成元，构成数组ans[]使得ans[i]就是i的最小生成元，然后查找即可

一次性枚举是，是已知生成元x求y,而非已知y求x,后者的效率很慢

```c
#include <stdio.h>
#define maxn 100005
int ans[maxn] = {0}; /*将ans的所有元素初始化为零*/

int main()
{
    /*使ans[i]是i的最小生成元*/
    char s[10];
    for (int m = 1;m < maxn;m++)
    {
        int y = m;
        sprintf(s,"%d",m);
        for (int i = 0;s[i]!='\0';i++) y+=s[i]-'0';

        if(ans[y]== 0) ans[y] = m; 
    }

    int T,n;
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d",&n);
        printf("%d\n",ans[n]);
    }
    return 0;
}

```

