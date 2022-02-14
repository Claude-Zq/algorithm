

用cin输入果然还是太慢了

```c++
#include<fstream>
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

struct student {
	string id, name;
	int score;
};

bool cmp1(const student& a, const student& b) {
	return a.id < b.id;
}

bool cmp2(const student& a, const student& b) {
	int temp = strcmp(a.name, b.name);
	if (temp != 0) return temp < 0;
	else return a.id < b.id;
}

bool cmp3(const student& a, const student& b) {
	if (a.score != b.score) return a.score < b.score;
	else return a.id < b.id;
}

int main() {

	int n, c,kcase = 0;
	while (cin >> n >> c && n) {
		vector<student> v(n);
		for (int i = 0; i < n; i++) cin >> v[i].id >> v[i].name >> v[i].score;
		if (c == 1) sort(v.begin(), v.end(), cmp1);
		else if (c == 2) sort(v.begin(), v.end(), cmp2);
		else if (c == 3) sort(v.begin(), v.end(), cmp3);

		cout << "Case " << ++kcase << ':' << endl;
		for (int i = 0; i < n; i++)
			cout << v[i].id << ' ' << v[i].name << ' ' << v[i].score << endl;
	}

	return 0;
}
```







```c++
#include<cstdio>
#include<vector>
#include<algorithm>
#include<cstring>
using namespace std;

const int maxn = 10; /*名字的最大长度*/

struct student {
	char name[maxn];
	int id,score;
};

bool cmp1(const student& a, const student& b) {
	return a.id < b.id;
}

bool cmp2(const student& a, const student& b) {
	int temp = strcmp(a.name, b.name);
	if (temp != 0) return temp < 0;
	else return a.id < b.id;
}

bool cmp3(const student& a, const student& b) {
	if (a.score != b.score) return a.score < b.score;
	else return a.id < b.id;
}

int main() {
	int n, c,kcase = 0;
	while (scanf("%d %d", &n, &c) == 2 && n) {
		vector<student> v(n);
		for (int i = 0; i < n; i++) scanf("%d %s %d", &v[i].id, v[i].name, &v[i].score);
        /*分情况排序*/
		if (c == 1) sort(v.begin(), v.end(), cmp1);
		else if (c == 2) sort(v.begin(), v.end(), cmp2);
		else if (c == 3) sort(v.begin(), v.end(), cmp3);
		/*输出*/
		printf("Case %d:\n", ++kcase);
		for (int i = 0; i < n; i++)  printf("%06d %s %d\n", v[i].id, v[i].name, v[i].score);
	}
	return 0;
}
```

