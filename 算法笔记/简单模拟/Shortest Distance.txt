```c++
#include<cstdio>
#include<vector>
#define min(a,b) (a < b? a:b)
#define max(a,b) (a > b? a:b) /*宏*/

int main() {

	int n, m, sum = 0;
	scanf("%d", &n);
	std::vector<int> v(n);
	for (int i = 0; i < n; i++) { scanf("%d", &v[i]); sum += v[i]; }
	scanf("%d", &m);
	while (m--) {
		int sum1 = 0, sum2 = 0;
		int e1, e2;
		scanf("%d %d", &e1, &e2);
		for (int i = min(e1, e2) - 1,end = max(e1, e2) - 1; i < end; i++) sum1 += v[i];
		sum2 = sum - sum1;
        
		printf("%d\n", min(sum1, sum2));
	}


	return 0;
}
```



```c++
#include<cstdio>
#include<vector>
#define min(a,b) (a < b? a:b)
#define max(a,b) (a > b? a:b)

int main() {

	int n, m, sum = 0;
	scanf("%d", &n);
	std::vector<int> v(n+2);/*v[i]是出口1到出口i的距离*/
	v[1] = 0;
	for (int i = 2; i <=n+1; i++) { scanf("%d", &v[i]); sum += v[i]; v[i] += v[i - 1]; }
	scanf("%d", &m);
	while (m--) {
		int sum1 = 0, sum2 = 0;
		int e1, e2;
		scanf("%d %d", &e1, &e2);
		sum1 = v[max(e1, e2)] - v[min(e1, e2)];
		sum2 = sum - sum1;

		printf("%d\n", min(sum1, sum2));
	}


	return 0;
}
```

