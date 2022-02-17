



```c++
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;

int main()
{
	int l, n;
	while (scanf("%d %d", &l, &n) == 2) {
		vector<int> v(n);
		for (int i = 0; i < n; i++) scanf("%d", &v[i]);
        
		sort(v.rbegin(), v.rend());/*降序排列*/

		int ans = 0;/*计算答案*/
		for (int i = 0; i < n && l>0; i++,ans++) l -= v[i];

		if (l > 0) printf("impossible\n");
		else printf("%d\n", ans);
	}
	return 0;
}
```

