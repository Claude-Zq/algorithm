## Ananagrams

### Q

输入一些单词（以“#”为结束标志），找出所有满足如下条件的单词：该单词不能通过字母的重排，得到输入文本中的另一个单词。在判断是否满足条件是不分大小写，但是在输出时应保留输入时的大小写，按字典序进行排列（所有大写字母在所有小写字母前面）。 

input 

ladder came tape soon leader acme RIDE lone Dreis peat
 ScAlE orb  eye  Rides dealer  NotE derail LaCeS  drIed
noel dire Disk mace Rob dries
#

output

Disk
NotE
derail
drIed
eye
ladder
soon

解题关键：将单词标准化，解决字母重排问题

优化：相比原作，用了两个map,由于将每个单词的标准串都存储到A中，减少了对标准串的重复计算

### A A2

```c++
#include <fstream>
#include<string>
#include<map>
#include<algorithm>

/*将s的每个字母转换为小写,并排序*/
std::string STD(std::string s){
	for (int i = 0; i < s.length(); i++){
		s[i] = tolower(s[i]);
	}
	std::sort(s.begin(), s.end());
	return s;
}


int main()
{
	std::ifstream ifs;
	std::ofstream ofs;
	/*打开文件*/
	ifs.open("input.txt", std::ios::in);
	ofs.open("output.txt", std::ios::out | std::ios::trunc);

	std::map<std::string, std::string> A;
	std::map<std::string, int> B;

	std::string s;
	while (ifs >> s && s != "#")
	{
		std::string stds = STD(s);
		A.insert(std::pair<std::string, std::string>(s, stds));
		if (B.count(stds)) B[stds]++;/*该字符的标准串在B中已经出现*/
		else B[stds] = 1;/*比下面的代码简洁*/
		//else B.insert(std::pair<std::string, int>(stds, 1));
	}
    
	/*输出答案*/
	for (std::map<std::string, std::string>::iterator it = A.begin(); it != A.end(); it++) {
		if (B[it->second] == 1)  ofs << it->first << std::endl; /*如果该字串的标准串只出现过一次*/
	}

	/*关闭文件*/
	ifs.close();
	ofs.close();
	return 0;
}
```
