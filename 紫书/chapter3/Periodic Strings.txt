**周期串（Periodic Strings, UVa455）**
如果一个字符串可以由某个长度为k的字符串重复多次得到，则称该串以k为周期。 例如，abcabcabcabc以3为周期（注意，它也以6和12为周期）。输入一个长度不超过80的字符串，输出其最小周期。



### 代码

```c
#include <stdio.h>
#include <string.h>

/*函数功能：判断T是不是长度是len的字符串周期*/
//将len放在参数列表而不是在函数体中，防止拖慢速度
int JudgeT(char s[],int len,int T)
{
    if (len % T != 0) return 0; /*如果长度不是周期的整数倍*/
    for (int i = T;i < len;i++) if(s[i%T]!= s[i]) return 0;
    return 1;
}

int main()
{
    int n;
    scanf("%d",&n);

    while(n--)
    {
       char s[100];
       scanf("%s",s);
       int len = strlen(s);
       for (int T = 1;T <=len;T++)
       {
           if (JudgeT(s,len,T)){printf("%d\n",T);break;}
       }
    }
    return 0;
}

```
