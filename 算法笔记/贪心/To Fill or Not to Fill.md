

# **To Fill or Not to Fill** 



## 坑

double类型在输入时必须用%lf,不能用%f



## 思路

### 关键点

* 每个加油站可以抽象成一个区间，范围是其所在位置到加满有后能走到的位置
* 要想油价最低，从便宜的油尽可能多用
* 对于油价(float类型)相同的一段路，不能简单的累加油价，而是统计好路的长度后按(油价*路程长度)计算，否则会有浮点误差

### 具体实现

* 判断是否能够走到终点：先将这些区间(加油站)按始端升序排列，判断每个区间的末端是否达到下一个区间的始端，若没有，则不能到达终点

* 计算最低价：先将这些区间(加油站)按价格降序排列，遍历数组，为每公里路标上油价，从而让低油价覆盖高油价



# 代码实现

```c++
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;


struct station {
	int begin, end;
	float price;
};

bool cmp1(const station& a, const station& b) {
	return a.begin < b.begin;
}
bool cmp2(const station& a, const station& b) {
	return a.price > b.price;
}
	
int main()
{
	
	int c, d, avg, n;
	scanf("%d %d %d %d", &c, &d, &avg, &n);

	vector<station> v(n);

	for (int i = 0; i < n; i++) {
		scanf("%f %d", &v[i].price, &v[i].begin);
		v[i].end = v[i].begin + c * avg;    /*终点等于起点+加满油能走的距离*/
	}

	sort(v.begin(), v.end(), cmp1);/*按起点位置升序排列*/

    /*判断是否能走到终点*/
	int x = 0;
	for (int i = 0; i < n && x < d; i++) {
		if (v[i].begin > x) break;
		x = v[i].end;
	}
	if (x < d) { printf("The maximum travel distance = %.2f\n", (double)x); return 0; }

	vector<int> Road(d); /*第i+1公里的最低油费价为v[Road[i]]*/
	sort(v.begin(), v.end(), cmp2); /*按油价降序排列*/

	for (int i = 0; i < n; i++) 
		fill(Road.begin() + v[i].begin, Road.begin() + min(v[i].end, d), i);

	float ans = 0;
	for (int i = 0; i < d; i++) {
		int cnt = 1;
		while (i + 1 < d && Road[i + 1] == Road[i]) { cnt++; i++; }
		ans += v[Road[i]].price * cnt; /*将油价相同的一段合起来算，不然会有浮点误差*/
	}
	ans /= avg;

	printf("%.2f\n", ans);
    
	return 0;
}
```



# 改进版

更新了判断能否到达终点的方法，只需要一次排序

```c++
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;

struct station {
	int begin, end;
	float price;
};

bool cmp(const station& a, const station& b) {
	return a.price > b.price;
}

int main()
{

	int c, d, avg, n;
	scanf("%d %d %d %d", &c, &d, &avg, &n);

	vector<station> v(n);

	for (int i = 0; i < n; i++) {
		scanf("%f %d", &v[i].price, &v[i].begin);
		v[i].end = v[i].begin + c * avg;    /*终点等于起点+加满油能走的距离*/
	}

	vector<int> Road(d); /*第i+1公里的最低油费价为v[Road[i]]*/

	fill(Road.begin(), Road.end(), -1);

	sort(v.begin(), v.end(), cmp); /*按油价降序排列*/

	for (int i = 0; i < n; i++) /*为每段路添上油价*/
		fill(Road.begin() + v[i].begin, Road.begin() + min(v[i].end, d), i);

	float ans = 0;
	for (int i = 0; i < d; i++) {
		if (Road[i] == -1) { /*没填油价，说明走不到下一公里*/
			printf("The maximum travel distance = %.2f\n", (double)i);
		return 0;
		}
		int cnt = 1;
		while (i + 1 < d && Road[i + 1] == Road[i]) { cnt++; i++; }
		ans += v[Road[i]].price * cnt; /*将油价相同的一段合起来算，不然会有浮点误差*/
	}
	ans /= avg;

	printf("%.2f\n", ans);

	return 0;
}
```

