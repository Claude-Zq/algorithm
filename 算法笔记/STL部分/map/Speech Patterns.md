

有bug版

```c++
#include<iostream>
#include<string>
#include<unordered_map>
#include<cctype>
using namespace std;


int main()
{
	string word;
	unordered_map<string, int> m;
    
	while (cin >> word) {
		/*去掉尾部部标点*/
		while (word.size() > 0 && !isalpha(word.back()) && !(isdigit(word.back()))) word.pop_back();
		/*去掉首部部标点*/
		while (word.size() > 0 && !isalpha(word.front()) && !(isdigit(word.front()))) word.erase(word.begin());

		if (word.size() == 0) continue;/*整个word都是标点*/

		/*全部转小写*/
		for (auto it = word.begin(); it != word.end(); it++) *it = tolower(*it);
		
		auto pun = word.begin();
		while (pun != word.end()) {
			if(!isalpha((*pun)) && !isdigit((*pun))) break;
			pun++;
		}
		if (pun == word.end()) m[word]++;
		else {
			m[word.substr(0, pun - word.begin())]++; /*标点前的单词*/
			m[word.substr(pun - word.begin()+1, word.end() - pun)];/*标点后的单词*/
		}
	}
	auto ans = m.begin();
	for (auto it = m.begin(); it != m.end(); it++) {
		if (it->second > ans->second) ans = it;
		else if (it -> second == ans->second) { if (it->first < ans->first)ans = it; }
	}
	cout << ans->first << " " << ans->second << endl;
	
	return 0;
}
```



把stirng作为流进行读写

```c++
#include<iostream>
#include<string>
#include<unordered_map>
#include<cctype>
#include<sstream>
using namespace std;

int main()
{
	string line;
	getline(cin, line);
	unordered_map<string, int> m;

	for (auto it = line.begin(); it != line.end(); it++) {
		if (isalpha(*it)) *it = tolower(*it); /*字母换为小写*/
		else if (isdigit(*it)); 
		else *it = ' ';/*标点换为空格*/
	}
	stringstream ss(line);
	string word;
	while (ss >> word) m[word]++;
    
	auto ans = m.begin();
	for (auto it = m.begin(); it != m.end(); it++) {
		if (it->second > ans->second) ans = it;
		else if (it->second == ans->second) { if (it->first < ans->first) ans = it; }
	}
	cout << ans->first << " " << ans->second << endl;
	return 0;
}
```

