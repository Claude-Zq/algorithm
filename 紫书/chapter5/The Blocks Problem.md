## The Blocks Problem

### Q

输入n，得到编号为0~n-1的木块，分别摆放在顺序排列编号为0~n-1的位置。现对这些木块进行操作，操作分为四种。

1、move a onto b：把木块a、b上的木块放回各自的原位，再把a放到b上；

2、move a over b：把a上的木块放回各自的原位，再把a发到含b的堆上；

3、pile a onto b：把b上的木块放回各自的原位，再把a连同a上的木块移到b上；

4、pile a over b：把a连同a上木块移到含b的堆上。

当输入quit时，结束操作并输出0~n-1的位置上的木块情况

Sample Input 
10
move 9 onto 1
move 8 over 1
move 7 over 1
move 6 over 1
pile 8 over 6
pile 8 over 5
move 2 over 1
move 4 over 9
quit
Sample Output 
 0: 0
 1: 1 9 2 4
 2:
 3: 3
 4:
 5: 5 8 7 6
 6:
 7:
 8:
 9:

### A A3

version 1

```c++
#pragma warning(disable:4996)/*解决fopen、fscanf 在VS中要求替换为fopen_s、fscanf_s*/
#include<vector>
#include <cstdio>
using namespace std;


/*找出木块a在Wood中的行数*/
int get_i(vector<vector<int>>& Wood, int a){
	return Wood[a][0] == -1 ? Wood[a][1] : Wood[a][0];
}
/*找出木块a在Wood中的列数*/
int get_j(vector<vector<int>>& Wood, int a){
	int i = get_i(Wood, a);
	for (int j = 0; j < Wood[i].size(); j++) { if (Wood[i][j] == a) return j; }
	return -1;
}

/*将木块a上方的木块归位*/
void reset_above(vector<vector<int>>& Wood, int a){
	int i = get_i(Wood, a);
	int j = get_j(Wood, a);
	for (int k = Wood[i].size()-1; k > j; k--) {
		Wood[Wood[i][k]][0] = Wood[i][k];
		Wood[Wood[i][k]].pop_back();
		Wood[i].pop_back();
	}
}

/*操作move a onto b*/
void MN(vector<vector<int>>& Wood, int a, int b)
{
	/*把a、b上方的木块归位*/
	reset_above(Wood, a);
	reset_above(Wood, b);
	int ia = get_i(Wood, a);
	int ib = get_i(Wood, b);
	Wood[ib].push_back(a); /*把a放到b上*/
	Wood[ia].pop_back();
	if (Wood[ia].size() == 0) { Wood[ia].push_back(-1); Wood[ia].push_back(ib); }/*如果a在原位*/
}

/*操作move a over b*/
void MV(vector<vector<int>>& Wood, int a, int b)
{
	reset_above(Wood, a);
	int ia = get_i(Wood, a);
	int ib = get_i(Wood, b);

	Wood[ib].push_back(a);
	Wood[ia].pop_back();
	if (Wood[ia].size() == 0) { Wood[ia].push_back(-1); Wood[ia].push_back(ib); }/*如果a在原位*/
}

/*操作pile a onto b*/
void PN(vector<vector<int>>& Wood, int a, int b)
{
	reset_above(Wood, b);
	int ib = get_i(Wood, b);
	int ia = get_i(Wood, a), ja = get_j(Wood, a);
	for (int j = ja; j < Wood[ia].size(); j++) Wood[ib].push_back(Wood[ia][j]); /*移到b上*/
	for (int j = Wood[ia].size() - 1; j >= ja; j--)Wood[ia].pop_back(); /*擦掉原位*/
	if (Wood[ia].size() == 0) { Wood[ia].push_back(-1); Wood[ia].push_back(ib); }
}

/*操作pile a over b*/
void PV(vector<vector<int>>& Wood, int a, int b)
{
	int ib = get_i(Wood, b);
	int ia = get_i(Wood, a), ja = get_j(Wood, a);
	for (int j = ja; j < Wood[ia].size(); j++) Wood[ib].push_back(Wood[ia][j]); /*移到b上*/
	for (int j = Wood[ia].size() - 1; j >= ja; j--)Wood[ia].pop_back(); /*擦掉原位*/
	if (Wood[ia].size() == 0) { Wood[ia].push_back(-1); Wood[ia].push_back(ib); }
}


int main()
{
    FILE* fin = fopen("input.txt", "r");
	FILE* fout = fopen("output.txt", "w");

	int n;
	fscanf(fin, "%d", &n);

	vector<vector<int>> Wood;
	Wood.resize(n);
	/*初始化放木块的vector*/
	for (int i = 0; i < n; i++) Wood[i].push_back(i);
    
	char s1[10], s2[10];
	int a, b;

	/*执行操作*/
	while (fscanf(fin, "%s %d %s %d", s1, &a, s2, &b) == 4)
	{
		if (get_i(Wood, a) == get_i(Wood, b)) continue; /*如果a,b在同一堆*/
		if (s1[0] == 'm' && s2[1] == 'n') MN(Wood, a, b);
		else if(s1[0] == 'm' && s2[1] == 'v') MV(Wood, a, b);
		else if(s1[0] == 'p' && s2[1] == 'n') PN(Wood, a, b);
		else if(s1[0] == 'p' && s2[1] == 'v') PV(Wood, a, b);
	}
	/*输出结果*/
	for (int i = 0; i < n; i++){
		fprintf(fout, "%d:", i);
		if (Wood[i][0] != -1) {
			for (int j = 0; j < Wood[i].size(); j++) {
				if (j) fprintf(fout, " ");
				fprintf(fout, "%d", Wood[i][j]);
			}
		}
		fputc('\n', fout);
	}


	fclose(fin);
	fclose(fout);
	return 0;
}
```

version 2

改进：

1.将Wood声明为全局变量，避免多次传参，较少代码量

2.提取出四种操作的共同点，减少重复代码

优点：

找木块的速度有提升：

原作：横标:O(n),纵标:O(n)

我的：横标O(1),纵坐标: O(n)

方法：木块a如果不在原位，则原位Wood[a]必定为空，所以原位的第一位插-1来表示木块不在，第二位记录其所在堆数的横标。另外，要找到纵标时，也可直接跳到对应堆，故速度也有所提升

```c++
#pragma warning(disable:4996)/*解决fopen、fscanf 在VS中要求替换为fopen_s、fscanf_s*/
#include<vector>
#include <cstdio>
using namespace std;
vector<vector<int>> Wood;


/*找出木块a在Wood中的行数*/
int get_i(int a) {
	return Wood[a][0] == -1 ? Wood[a][1] : Wood[a][0];
}

/*找出木块a在Wood中的列数*/
int get_j(int a) {
	int i = get_i(a);
	for (int j = 0; j < Wood[i].size(); j++) { if (Wood[i][j] == a) return j; }
	return -1;
}

/*将木块a上方的木块归位*/
void reset_above(int a) {
	int i = get_i(a);
	int j = get_j(a);
	for (int k = Wood[i].size() - 1; k > j; k--) {
		Wood[Wood[i][k]][0] = Wood[i][k];
		Wood[Wood[i][k]].pop_back();
		Wood[i].pop_back();
	}
}

/*操作pile a over b*/
void PV(int a, int b)
{
	int ib = get_i(b);
	int ia = get_i(a), ja = get_j(a);
	for (int j = ja; j < Wood[ia].size(); j++) Wood[ib].push_back(Wood[ia][j]); /*移到b上*/
	Wood[ia].resize(ja);
	if (Wood[ia].size() == 0) { Wood[ia].push_back(-1); Wood[ia].push_back(ib); }
}

int main()
{
	FILE* fin = fopen("input.txt", "r");
	FILE* fout = fopen("output.txt", "w");

	int n;
	fscanf(fin, "%d", &n);
	Wood.resize(n);

	/*初始化放木块的vector*/
	for (int i = 0; i < n; i++) Wood[i].push_back(i);
	char s1[10], s2[10];
	int a, b;

	/*录入操作并执行*/
	while (fscanf(fin, "%s %d %s %d", s1, &a, s2, &b) == 4)
	{
		if (get_i(a) == get_i(b)) continue; /*如果a,b在同一堆*/
		if (s1[0] == 'm') reset_above(a);
		if (s2[1] == 'n') reset_above(b);
		PV(a, b);
	}
	/*输出结果*/
	for (int i = 0; i < n; i++) {
		fprintf(fout, "%d:", i);
		if (Wood[i][0] != -1) {
			for (int j = 0; j < Wood[i].size(); j++) {
				if (j) fprintf(fout, " ");
				fprintf(fout, "%d", Wood[i][j]);
			}
		}
		fputc('\n', fout);
	}

	fclose(fin);
	fclose(fout);
	return 0;
}
```

