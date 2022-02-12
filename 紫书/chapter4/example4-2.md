#### 题目

刽子手游戏其实是一款猜单词游戏，如图4- 1所示。游戏规则是这样的：计算机想一个单词 让你猜，你每次可以猜一个字母。如果单词里有那个字母，所有该字母会显示出来；如果没有那 个字母，则计算机会在一幅“刽子手”画上填一 笔。这幅画一共需要7笔就能完成，因此你最多 只能错6次。注意，猜一个已经猜过的字母也算错。在本题中，你的任务是编写一个“裁判”程序，输入单词和玩家的猜测，判断玩家赢了 （You win.）、输了（You lose.）还是放弃了 （You chickened out.）。每组数据包含3行，第1 行是游戏编号（-1为输入结束标记），第2行是 计算机想的单词，第3行是玩家的猜测。后两行 保证只含小写字母。
测试样例：
1cheese chese
2cheese abcdefg
3cheese abcdefgij
1样例输出:
Round 1 You win.
Round 2 You chickened out.
Round 3 You lose.


#### 代码

```c
#include <stdio.h>
#include<string.h>


/*统计长为n的字符串s各个字母的个数于数组N中*/
void CountAlpha(char *s,int n,int *N){
    for (int i = 0;i < n;i++) N[s[i]-'a']++;
}


int main()
{
    FILE *fin = fopen("input.txt","r");
    FILE *fout = fopen("output.txt","w");

    int T,kcase = 0;
    int ANS[26],GUS[26];
    char s[50];
    const char* msg[] = {"You win.","You lose.","You chickened out."};
    while(fscanf(fin,"%d",&T)==1&&T!=-1)
    {
        /*清一下*/
        memset(ANS,0,sizeof(ANS));
        memset(GUS,0,sizeof(GUS));
        /*输入答案字符串*/
        fscanf(fin,"%s",s);
        CountAlpha(s,strlen(s),ANS);/*统计*/

        /*输入玩家猜的字符串*/
        fscanf(fin,"%s",s);
        CountAlpha(s,strlen(s),GUS);/*统计*/

        int ans = 0;/*默认玩家猜对*/
        int error = 0;/*猜错次数*/
        for(int i = 0;i < 26;i++){
            /*猜错*/
            if(!ANS[i]&&GUS[i]){error += GUS[i];}
            /*猜漏*/
            else if(ANS[i]&&!GUS[i]) ans = 2;
            /*猜对*/
            else if(ANS[i]&&GUS[i]) {if(GUS[i]>1) error += GUS[i] - 1;/*猜重复*/}
            /*猜错7次*/
            if(error >= 7) {ans = 1;break;}
        }
		/*输出结果*/
        fprintf(fout,"Round %d\n%s\n",++kcase,msg[ans]);
    }

    fclose(fin);
    fclose(fout);

    return 0;
}

```

### 