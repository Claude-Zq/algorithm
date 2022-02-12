```c++
#include<cstdio>
#include<vector>

int main() {
	
	int N;
	while (scanf("%d", &N) == 1 && N != 0) {
		std::vector<int> v(N);
		for (int i = 0; i < N; i++) scanf("%d", &v[i]);
		int x,ans = -1;
		scanf("%d", &x);
		for (int i = 0; i < N; i++) if (v[i] == x) { ans = i; break; }
		printf("%d\n", ans);
	}
	return 0;
}
```

