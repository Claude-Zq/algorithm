```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;

int main() {
	
	string sa, sb;
	while (cin >> sa >> sb) {
		/*去掉逗号*/
		for (auto it = sa.begin(); it != sa.end(); it++) if (*it == ',') { sa.erase(it); it--; }
		for (auto it = sb.begin(); it != sb.end(); it++) if (*it == ',') { sb.erase(it); it--; }
		int A, B;
		sscanf(sa.c_str(), "%d", &A);
		sscanf(sb.c_str(), "%d", &B);
		printf("%d\n", A + B);
	}
	
	return 0;
}
```

