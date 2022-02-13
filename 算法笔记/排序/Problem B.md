



```c++
#include<cstdio>
#include<algorithm>
using namespace std;
const int maxn = 10;

int M[maxn][maxn], S[2 * maxn + 5];

bool cmp(int a, int b) {
	return a > b;
}

int main() {

	int m;
	while(scanf("%d", &m)==1&&m){
        int index = -1;
        for (int i = 0; i < m; i++) {
		int sum = 0; /*每行的和*/
		for (int j = 0; j < m; j++) {
			scanf("%d", &M[i][j]);
			sum += M[i][j];
		}
		S[++index] = sum;
	}
	/*每列的和*/
	for (int c = 0; c < m; c++) {
		int sum = 0;
		for (int r = 0; r < m; r++) sum += M[r][c];
		S[++index] = sum;
	}

    /*主对角线*/
	int sum = 0;
	for (int i = 0; i < m; i++) sum += M[i][i];
	S[++index] = sum;
    
    /*副对角线*/
	sum = 0;
	for (int i = 0, j = m - 1; i < m; i++, j--) sum += M[i][j];
	S[++index] = sum;

	sort(S, S + 2 * m + 2,cmp);

	for (int i = 0; i < 2 * m + 2; i++) {
		if (i) putchar(' ');
		printf("%d", S[i]);
	}
    printf("\n");
    }
	
	return 0;
}

```

