#### 时间：2022/1/23

#### 作者：周青

#### 内容：判断回文串和镜像串

```c
#include <stdio.h>
#include <string.h>

/*判断字符串是否是回文*/
//是：1
//不是：0
int IsPal(char s[])
{
    char *pE = s,*pB = s;
    while (*(pE+1) != '\0') pE++; /*pE指向s的末尾*/

    while (pB < pE)
    {
        if(*pB != *pE) return 0;
        pB++;pE--;
    }
    return 1;
}


//判断字符串是否是镜像
//是：1
//不是：0

int IsMirr(char s[])
{
    char ls[] ="AEHIJLMOSTUVWXYZ12358A3HILJMO2TUVWXY51SEZ8";
    char *pB=s,*pE = s;
    while(*(pE+1)!='\0') pE++; /*指向s的最后一个字母*/

    while(pB < pE)
    {
        char *pos = strchr(ls,*pB);
        if (pos == NULL) return 0;
        if (*(pos+strlen(ls)/2)!= *pE) return 0;
        pB++;pE--;
    }
    return 1;

}


void test01()
{
    char s[30];
    int first = 1;
    while(scanf("%s",s)== 1)
    {
        int p,m;
        p = IsPal(s);
        m = IsMirr(s);

        /*除第一行外换行*/
        if(first) first = 0;
        else printf("\n");

        printf("%s",s);
        if(!p && !m) printf("-- is not a palindrome\n");
        else if(p &&!m) printf("-- is a regular palindrome\n");
        else if(!p && m) printf("-- is a mirrored string\n");
        else if (p && m) printf("-- is a mirrored palindrome\n");
    }
}

int main()
{
    test01();
    return 0;
}

```

