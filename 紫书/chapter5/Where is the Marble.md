## Where is the Marble?

### Q

现有N个大理石，每个大理石上写了一个非负整数、首先把各数从小到大排序；然后回答Q个问题。每个问题问是否有一个大理石写着某个整数x，如果是，还要回答哪个大理石上写着x。排序后的大理石从左到右编号为1~N。
(在样例中，为了节约篇幅，所有大理石的数合并到一行，所有问题也合并到一行。)

**样例输入：**
4 1
2 3 5 1
5
5 2
1 3 3 3 1
2 3

**样例输出：**
CASE# 1：
5 found at 4
CASE# 2：
2 not found

3 found at 3 



### A A1

```c++
#pragma warning(disable:4996)/*解决fopen、fscanf 在VS中要求替换为fopen_s、fscanf_s*/
#include<vector>
#include<algorithm>
#include <cstdio>
using namespace std;

int main()
{
	FILE* fin = fopen("input.txt", "r");
	FILE* fout = fopen("output.txt", "w");

	int N, Q;
	int kcase = 0;
	while (fscanf(fin,"%d %d",&N,&Q)==2) {
		vector<int> M;
		/*输入大理石上的数字*/
		for (int i = 0; i < N; i++)
		{
			int digit;
			fscanf(fin,"%d", &digit);
			M.push_back(digit);
		}
		/*升序排列*/
		sort(M.begin(), M.end());
		/*输入问题*/
		fprintf(fout, "CASE# %d:\n", ++kcase);
		for (int i = 0; i < Q; i++) {
			int q;
			fscanf(fin, "%d", &q);
			vector<int>::iterator pos = find(M.begin(), M.end(), q);
            /*输出答案*/
			if (pos == M.end()) fprintf(fout, "%d not found\n", q);/*没找到*/
			else fprintf(fout, "%d found at %d\n", q, (int)(pos - M.begin()) + 1);/*找到了*/
		}
	
	}

	fclose(fin);
	fclose(fout);
	return 0;
}
```
