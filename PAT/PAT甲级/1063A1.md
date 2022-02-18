



```c++
#include<cstdio>
#include<vector>
#include<algorithm>
#include<set>
using namespace std;

#define ALL(x) x.begin(),x.end()
#define INS(x) inserter(x,x.begin())

int main()
{
	int n;
	scanf("%d", &n);
	vector<set<int> > vs(n + 1);

	for (int i = 1; i <= n; i++) {
		int m,temp;
		scanf("%d", &m);
		while (m--) {
			scanf("%d", &temp);
			vs[i].insert(temp);
		}
	}
	int k;
	scanf("%d", &k);
	while (k--) {
		int a, b;
		scanf("%d %d", &a, &b);
		set<int> in, un;
		set_intersection(ALL(vs[a]), ALL(vs[b]), INS(in));/*求交集*/
		set_union(ALL(vs[a]), ALL(vs[b]), INS(un));/*求并集*/
		printf("%.1f%%\n", 100.0 * in.size() /un.size());
	}
	return 0;
}
```

