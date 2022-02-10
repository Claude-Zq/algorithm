```c++
#include<iostream>
#include<string>
#include<algorithm>
using namespace std;

int main() {
	string A, B;
	int DA, DB;
	while (cin >> A >> DA >> B >> DB) {
		int cntA = count(A.begin(), A.end(), '0' + DA);
		int cntB = count(B.begin(), B.end(), '0' + DB);
		int PA = 0, PB = 0;
		while (cntA--) PA = PA * 10 + DA;
		while (cntB--) PB = PB * 10 + DB;
		printf("%d\n", PA + PB);
	}
	return 0;
}
```

