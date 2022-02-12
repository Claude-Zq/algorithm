#### 题目

给定两个长度相同且不超过100的字符串，判断是否能把其中一个字符串的各个字母重排，然后对26个字母做一个一一映射，使得两个字符串相同。
例如，JWPUDJSTVP重排后可以得到WJDUPSJPVT，然后把每个字母映射到它前一个字母（B->A,V->B,…,Z->Y,A->Z），得到VICTORIOUS。输出两个字符串，输出YES或者NO。

Sample Input
JWPUDJSTVP
VICTORIOUS
Sample Output
YES
Source
Northeastern Europe 2004

#### 代码

注意：输入文件每行均以\n结尾，否则运行结果有问题

```c
#include <stdio.h>
#include<string.h>
#include<stdlib.h>
#define maxn 105

/*降序排列谓词*/
int cmp(const void *a,const void *b){
    return  *(int*)b-*(int*)a;
}

/*记录长度为n字符串s中各个字母出现的次数*/
void Record(char *s,int n,int *cnt)
{
    for(int i = 0;i<n;i++) cnt[s[i]-'A']++;
}

int main()
{
    FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");
    char s[maxn];
    int cnt1[26]= {0},cnt2[26] = {0};

    //输入第一个字符串
    fgets(s,maxn,fin);
    Record(s,strlen(s)-1,cnt1); /*统计*/
    qsort(cnt1,sizeof(cnt1)/sizeof(int),sizeof(int),cmp);/*排序*/

    //输入第二个字符串
    fgets(s,maxn,fin);
    Record(s,strlen(s)-1,cnt2); /*统计*/
    qsort(cnt2,sizeof(cnt2)/sizeof(int),sizeof(int),cmp);/*排序*/

    int ok = 1;
    for (int i = 0;i < 26;i++){
        if(cnt1[i]!=cnt2[i]){ok = 0;break;}
        if(cnt1[i]==0||cnt2==0)break;
    }

    if(ok) fprintf(fout,"YES\n");
    else fprintf(fout,"NO\n");

    fclose(fin);
    fclose(fout);
    return 0;
}

```

