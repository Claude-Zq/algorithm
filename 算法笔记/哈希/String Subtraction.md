



```c++
#include<iostream>
#include<string>
using namespace std;

bool cnt[300];

int main() {

	string s1,s2;
    
	getline(cin, s1);
	getline(cin, s2);

	for (auto it = s2.begin(); it != s2.end(); it++) cnt[*it] = true;
	for (auto it = s1.begin(); it != s1.end(); it++) if (!cnt[*it]) cout.put(*it);

	return 0;
}
```

