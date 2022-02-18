



```c++
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;

/*根据题目中名的特殊性，将其转化为数字*/
int getId(char* name) {
	int id = 0;
	for (int i = 0; i < 3; i++) id = id * 26 + name[i] - 'A';
	id = id * 10 + name[3] - '0';
	return id;
}
/*将Id转回Name*/
void getName(int id, char* name) {
	name[4] = '\0';
	name[3] = id % 10 + '0';
	id /= 10;
	for (int i = 2; i >= 0; i--) {
		name[i] = id % 26 + 'A';
		id /= 26;
    }
	return;
}

int main()
{
	int n, k;
	scanf("%d %d", &n, &k);
	vector<vector<int> >v(k+1);

	while (n--) {
		char name[10];
		int c,course;
		scanf("%s %d", name, &c);
		int id = getId(name);
		while (c--) { 
            scanf("%d", &course);
            v[course].push_back(id);}
	}
	for (int i = 1; i <= k; i++) {
		printf("%d %d\n", i, v[i].size());
		sort(v[i].begin(), v[i].end());
		char name[10];
		for (auto it = v[i].begin(); it != v[i].end(); it++) {
			getName(*it, name);
			printf("%s\n", name);
		}
	}
	return 0;
}
```



简单粗暴/超时版

```c++
#include<vector>
#include<algorithm>
#include<iostream>
#include<string>
using namespace std;

int main()
{
	int n, k;
	cin >> n >> k;
	vector<vector<string> >v(k+1);

	while (n--) {
		string name;
		int c,course;
		cin >> name >> c;
		while (c--) {
			cin >> course;
			v[course].push_back(name);
		}
	}

	for (int i = 1; i <= k; i++) {
		cout << i << ' ' << v[i].size() << endl;
		sort(v[i].begin(), v[i].end());
		for (auto it = v[i].begin(); it != v[i].end(); it++) 	cout << *it << endl;
	}

	return 0;
}
```

