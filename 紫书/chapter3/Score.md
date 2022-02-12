### 题目

给出一个由O和X组成的串（ 长度为1～ 80） ， 统计得分。 每个O的得分为目前连续出现
的O的个数， X的得分为0。 例如， OOXXOXXOOO的得分为1+2+0+0+1+0+0+1+2+3。

### 代码

```d
#include <stdio.h>
#include <string.h>

int main()
{
    char s[100];
    int score = 0,count = 0;

    scanf("%s",s);
    int n = strlen(s);
    for(int i = 0;i < n;i++)
    {
        if (s[i]=='O')  score += (++count);
        else count = 0;
    }
    printf("%d",score);
    return 0;
}

```

