## The SetStack Computer

### Q A3

  有一个专门为了集合运算而设计的“集合栈”计算机。该机器有一个初始为空的栈，并且支持以下操作：
PUSH：空集“{}”入栈
DUP：把当前栈顶元素复制一份后再入栈
UNION：出栈两个集合，然后把两者的并集入栈
INTERSECT：出栈两个集合，然后把二者的交集入栈
ADD：出栈两个集合，然后把先出栈的集合加入到后出栈的集合中，把结果入栈
       每次操作后，输出栈顶集合的大小（即元素个数）。例如栈顶元素是A={ {}， {{}} }， 下一个元素是B={ {}， {{{}}} }，则：
UNION操作将得到{ {}， {{}}， {{{}}} }，输出3.
INTERSECT操作将得到{ {} }，输出1
ADD操作将得到{ {}， {{{}}}， { {}， {{}} } }，输出3.
（输入：先输入测试次数，再输入操作次数，再输入具体操作）
Sample Input
2
9
PUSH
DUP
ADD
PUSH
ADD
DUP
ADD
DUP
UNION
5
PUSH
PUSH
ADD
PUSH
INTERSECT

Sample Output
0
0
1
0
1
1
2

***

0
0
1
0
0

***

### A

```c++
#include <fstream>
#include<set>
#include<stack>
#include<map>
#include<vector>
#include<algorithm>
#include<string>
using namespace std;

map<set<int>, int> IDcache;
vector<set<int>> Setcache;
stack<int> SSC;

/*输入一个集合，返回其在Setcache的下标，如果没有则创建一个*/
int ID(set<int> s){
	if (IDcache.count(s)) return(IDcache[s]);
	else {
		Setcache.push_back(s);
		return IDcache[s] = Setcache.size() - 1;
	}
}
int PUSH(){
	SSC.push(ID(set<int>()));
	return 0;
}
int DUP() {
	SSC.push(SSC.top());
	return Setcache[SSC.top()].size();
}

int UNION() {
	set<int> s1(Setcache[SSC.top()]); SSC.pop();
	set<int> s2(Setcache[SSC.top()]); SSC.pop();
	set<int> U;
	set_union(s1.begin(), s1.end(), s2.begin(), s2.end(), inserter(U, U.begin()));
	SSC.push(ID(U));
	return U.size();
}
int INTERSECT() {
	set<int> s1(Setcache[SSC.top()]); SSC.pop();
	set<int> s2(Setcache[SSC.top()]); SSC.pop();
	set<int> I;
	set_union(s1.begin(), s1.end(), s2.begin(), s2.end(), inserter(I, I.begin()));
	SSC.push(ID(I));
	return I.size();
}

int ADD() {
	set<int> s1(Setcache[SSC.top()]); SSC.pop();
	set<int> s2(Setcache[SSC.top()]); SSC.pop();
	s2.insert(ID(s1));
	SSC.push(ID(s2));
	return s2.size();
}


int main()
{
	std::ifstream ifs;
	std::ofstream ofs;
	/*打开文件*/
	ifs.open("input.txt", std::ios::in);
	ofs.open("output.txt", std::ios::out | std::ios::trunc);

	int T, n;
	ifs >> T;
	while (T--) {
		ifs >> n;
		string op;
		int ans;
		while (n--) {
			ifs >> op;
			if (op == "PUSH") ans = PUSH();
			else if (op == "DUP") ans = DUP();
			else if (op == "UNION") ans = UNION();
			else if (op == "INTERSECT") ans = INTERSECT();
			else if (op == "ADD") ans = ADD();
			else ans = -1;
			ofs << ans << endl;
		}
		ofs << "***" << endl;
		/*置空*/
		map<set<int>, int>().swap(IDcache);
		vector<set<int>>().swap(Setcache);
		stack<int>().swap(SSC);
	}

	/*关闭文件*/
	ifs.close();
	ofs.close();
	return 0;
}
```
