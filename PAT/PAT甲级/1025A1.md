





```c++
#include<cstdio>
#include<vector>
#include<algorithm>
#include<cstring>
using namespace std;

const int maxn = 15;

struct testee {
	char regi_num[maxn];
	int loc_num, loc_rank, score;
};

bool cmp(const testee& a, const testee& b) {
	if (a.score != b.score) return a.score > b.score;
	return strcmp(a.regi_num, b.regi_num) < 0;
}

int main() {

	int n;
	while (scanf("%d", &n) == 1) {
		int loc_num = 0;
		vector<testee> v;
		while (n--) {
			int k; loc_num++;
			scanf("%d", &k);
			vector<testee> local(k);
			for (int i = 0; i < k; i++) scanf("%s %d", local[i].regi_num, &local[i].score);
			sort(local.begin(), local.end(), cmp); /*分区内排序*/

			for (int i = 0, r = 1, pre = 0; i < k; i++) {
				if (local[i].score != pre) r = i + 1;
				local[i].loc_rank = r;
				local[i].loc_num = loc_num;
				v.push_back(local[i]);
				pre = local[i].score;
			}
		
		}

		sort(v.begin(), v.end(), cmp);/*最终排序*/
		printf("%d\n", v.size());
		for (int i = 0,r = 0,pre = -1; i < v.size(); i++) {
			if (v[i].score != pre) r = i + 1;
			printf("%s %d %d %d\n", v[i].regi_num, r, v[i].loc_num, v[i].loc_rank);
			pre = v[i].score;
		}
	}

	return 0;
}
```

