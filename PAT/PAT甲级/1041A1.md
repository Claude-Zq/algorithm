



```c++
#include<cstdio>
#include<vector>
#include<cstring>
using namespace std;

const int maxn = 10000+10;
int hashTable[maxn];

int main() {

	int n;
	while (scanf("%d", &n)==1){
		memset(hashTable, 0, sizeof(hashTable));
		vector<int> v(n);
		for (int i = 0; i < n; i++) {
			scanf("%d", &v[i]);
			hashTable[v[i]]++;
		}
		int flag = 0;
		for (int i = 0; i < n; i++) {
			if (hashTable[v[i]] == 1) {
				flag = 1;
				printf("%d\n", v[i]);
				break;
			}
		}
		if (!flag) printf("None\n");
	}

	return 0;
}
```

