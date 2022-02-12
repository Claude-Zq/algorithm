

```c++
#include<cstdio>

int main() {

	int m, A, B;
	while (scanf("%d %d %d", &m, &A, &B) == 3 && m) {
		long long sum = (long long)A + B; /*A要在相加前转好，不然*/
		int ans[40] = {0}, index = -1;
		do {
			ans[++index] = sum % m;
			sum /= m;
		} while (sum > 0);
		for (int i = index; i >= 0; i--) printf("%d", ans[i]);
		putchar('\n');
	}

	return 0;
}

```

