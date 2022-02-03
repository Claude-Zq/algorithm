## Andy's First Dictionary



### Q

样例输入
Adventures in Disneyland Two blondes were going to Disneyland when they came to a fork in the road. The sign read: "Disneyland Left.” So they went home.

样例输出
a
adventures
blondes
came
disneyland
fork
going
home
in
left
read
road
sign
so
the
they
to
two
went
were
when

### A3 

网上找的样例输入的双引号是中文("")的，在typora中和英文的引号("")一毛一样，浪费了半天时间排bug

```c++
#include <fstream>
#include<iostream>
#include<string>
#include<set>
#include<sstream>

int main()
{
	std::ifstream ifs;
	std::ofstream ofs;
	/*打开文件*/
	ifs.open("input.txt", std::ios::in);
	ofs.open("output.txt", std::ios::out | std::ios::trunc);


	std::string s,word;
	std::set<std::string> dict;
	
	while (ifs >> s){
		for (int i = 0; i < s.length(); i++) {
			if (isalpha(s[i])) s[i] = tolower(s[i]);
			else s[i] = ' '; /*将字符串s的字母换成小写，符号换为空格*/
		}
		/*将处理过的字符重新输入到words中*/
		std::stringstream ss(s); 
		while(ss >> word)dict.insert(word);
	}
	/*输出结果*/
	for (std::set<std::string>::iterator it = dict.begin(); it != dict.end(); it++)
	{
		ofs << *it << std::endl;
	}


	/*关闭文件*/
	ifs.close();
	ofs.close();
	return 0;
}
```
