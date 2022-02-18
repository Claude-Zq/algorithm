# 第一版 

缺点：空间复杂度大


```c++
#include<iostream>
#include<string>
#include<map>
#include<set>
#include<string>
using namespace std;

int main()
{
	int n, k;
	cin >> n >> k;
	map<string, set<int> > m;
	while (k--) {
		int course, num;
		string name;
		cin >> course >> num;
		while (num--) {
			cin >> name;
			m[name].insert(course);
		}
	}
	while (n--) {
		string name;
		cin >> name;
		cout << name << " " << m[name].size();
		for (auto it = m[name].begin(); it != m[name].end(); it++) {
			cout << " " << *it;
		}
		cout << endl;
	}
	return 0;
}
```



# 第二版

缺点：空间优于第一版，但依然很大

```c++
#include<vector>
#include<algorithm>
#include<iostream>
#include<string>
#include<unordered_map>
using namespace std;


int main()
{

	int n, k;
	cin >> n >> k;
	unordered_map<string, vector<int> > m;

	while (k--) {
		int course, num;
		string name;
		cin >> course >> num;
		while (num--) {
			cin >> name;
			m[name].push_back(course);
		}
	}
	while (n--) {
		string name;
		cin >> name;

		cout << name << " " << m[name].size();
		sort(m[name].begin(), m[name].end());
		for (auto it = m[name].begin(); it != m[name].end(); it++) {
			cout << " " << *it;
		}
		cout << endl;
	}

	return 0;
}

```



# 第三版

用到了散列(题目中的名字很特殊)

```c++
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;

const int maxn = 26 * 26 * 26 * 10 + 10 + 10;

/*根据题目中名的特殊性，将其转化为数字*/
int getId(char* name) {
	int id = 0;
	for (int i = 0; i < 3; i++) id = id * 26 + name[i] - 'A';
	id = id * 10 + name[3] - '0';
	return id;
}

vector<int> v[maxn];

int main()
{
	int n, k;
    char name[10];
	scanf("%d %d", &n, &k);
	while (k--) {
		int course, num;
		scanf("%d %d", &course, &num);
		while (num--) {
			scanf("%s", name);
			int id = getId(name);
			v[id].push_back(course);
		}
	}
	while (n--) {
		scanf("%s", name);
		int id = getId(name);
		printf("%s %d", name, v[id].size());
		sort(v[id].begin(), v[id].end());
		for (auto it = v[id].begin(); it != v[id].end(); it++) printf(" %d", *it);
		putchar('\n');
	}
	return 0;
}
```

