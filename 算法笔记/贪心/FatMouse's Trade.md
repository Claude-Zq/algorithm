

```c++
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;

struct room {
	int j, f;
	double unit;
};

bool cmp(const room& a, const room& b) {
	return a.unit > b.unit;
}

int main()
{
	int m, n;
	while (scanf("%d %d", &m, &n) == 2) {
		if (m == -1 || n == -1) break;
        
		vector<room> v(n);
		for (int i = 0; i < n; i++) {
			scanf("%d %d", &v[i].j, &v[i].f);
			v[i].unit = (double)v[i].j / v[i].f;
		}
		sort(v.begin(), v.end(), cmp);
        
		double ans = 0.0;
		for (int i = 0; i < n; i++) {
			if (m <= v[i].f) {ans += m * v[i].unit; break; }
			ans += v[i].j;
			m -= v[i].f;
		}
		printf("%.3f\n", ans);
	}
	return 0;
}
```

