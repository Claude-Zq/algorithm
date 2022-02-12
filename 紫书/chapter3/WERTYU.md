

```c
#include <stdio.h>
#include <string.h>

/*书上的答案*/
void test01()
{
    char s[] = "`1234567890-=qwertyuiop[]\\asdfghjkl;'zxcvbnm,./";
    int i,c;
    while ((c = getchar()) != EOF)
    {
        for (i = 1;s[i]&&s[i]!=c;i++);
        if(s[i]) putchar(s[i-1]);
        else putchar(c);
    }
}

/*我的答案*/
void test02()
{
    FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");

    char s[] =
 "`1234567890=qwertyuiop[]\\asdfghjkl;'zxcvbnm,./QWERTYUIOPASDFGHJKL;'ZXCVBNM";
    int c;
    char *pos;
    while ((c = fgetc(fin)) != EOF)
    {
        pos = strchr(s,c);
        if (pos == NULL) fputc(c,fout); /*没在s中，原样输出*/
        else fputc(*(pos-1),fout);
    }
    fclose(fin);
    fclose(fout);
}

int main()
{
    //test01();
    test02();
    return 0;
}

```

