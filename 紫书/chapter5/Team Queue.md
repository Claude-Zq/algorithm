## Team Queue

### Q

队列和优先级队列是大多数计算机科学家都知道的`数据结构`。但是团队队列却不被人熟知，尽管在生活中经常出现。比如，午餐时间的食堂门口的队列就是一个团队队列。在一个团队队列中，每个元素属于一个团队。如果一个元素进入一个队列，它首先从头到尾地搜寻这个队列——检查是否它的队友（在同一个团队称之为队友）也在这个队列里。如果有，它就排在它队友的后面（:-D就是插队咯~~）。如果没有，它就排在整个队列的最后，成为新的最后一名（/(ㄒoㄒ)/~真是不幸）。在普通队列中出队是这样的：元素从头到尾的被处理，按他们出现在团队队列里的顺序。你的任务是写一个程序模拟这样一个团队队列。

输入

输入文件会包含一个或多个测试样例。每一个测试样例由代表团队数量的t（1<=t<=1000）开始。然后t只团队描述如下，每一个团队由一个表示元素个数的数字，以及每个元素组成。元素属于整型，并且范围在0到999999（一百万减一）之间。一个团队可能有多达1000个元素。最后，指令列表如下。有三种不同的指令：ENQUEUE x——x进入团队队列。DEQUEUE x——处理第一个元素并将其移除STOP——结束一个测试样例。当t是0时，输入终止。警告：一个测试样例可能多达200000（/(ㄒoㄒ)/~~二十万）条指令，所以团队队列的实现应该是有效率的：入队和出队都应该花费常数时间。

输出

对应每个测试样例，首先输出一行“Scenario #k”，其中k表示第几次测试。然后，每一个“DEQUEUE”指令打印包含出队的元素（单独占一行）。打印一空行在每一个测试样例之后，即使是最后一个测试样例。
例如：
`Sample Input`

2
3 101 102 103
3 201 202 203
ENQUEUE 101
ENQUEUE 201
ENQUEUE
102
ENQUEUE 202
ENQUEUE 103
ENQUEUE
203
DEQUEUE
DEQUEUE
DEQUEUE
DEQUEUE
DEQUEUE
DEQUEUE
STOP
2
5
259001 259002 259003 259004 259005
6 260001 260002 260003 260004 260005
260006
ENQUEUE 259001
ENQUEUE 260001
ENQUEUE 259002
ENQUEUE
259003
ENQUEUE 259004
ENQUEUE 259005
DEQUEUE
DEQUEUE
ENQUEUE
260002
ENQUEUE
260003
DEQUEUE
DEQUEUE
DEQUEUE
DEQUEUE
STOP
0

Sample Output

Scenario
\#1
101
102
103
201
202
203

Scenario
\#2
259001
259002
259003
259004
259005
260001

关键：因为是根据团队扎堆排，所以以队员为单位的长队不是队列，而已团队整体为单位的长队才是一个队列。每个团队内部也有一个队列

细节：

入队时：队员x的团队是T，T内部的队列为空，则说明长队内没有T队的人，x只能排队尾，团队队列需要添加T

出队时：团队T的内部只剩一个独苗，出队后需要在团队队列中抹去T队

### A B

```c++
#include <fstream>
#include<map>
#include<vector>
#include<queue>
using namespace std;

int main()
{
	ifstream ifs;
	ofstream ofs;
	/*打开文件*/
	ifs.open("input.txt", ios::in);
	ofs.open("output.txt", ios::out | ios::trunc);

	int t, kcase = 0;
	while (ifs >> t && t != 0) {
		ofs << "Scenario #" << ++kcase << endl;
		map<int, int> MTT; /*member to team 由队员标号得到其团队的编号*/
		vector<queue<int>> QIT; /*团队内的队列构成的数组*/
        QIT.resize(t);
		queue<int> QOT;/*团队整体的队列*/
		/*输入队员编号，并为其分配团队编号*/
		for (int i = 0; i < t; i++) {
			int n, x;
			ifs >> n;
			while (n--) {ifs >> x; MTT[x] = i;}
		}
		/*执行操作*/
		string op;
		while (ifs >> op && op != "STOP") {
			if (op == "ENQUEUE") {
				int x;
				ifs >> x;
				int T = MTT[x];
				if (QIT[T].empty()) { QOT.push(T); QIT[T].push(x);}/*队列中没有和x一队的*/
				else QIT[T].push(x); /*队列中有和x一对的*/
			}
			else if (op == "DEQUEUE") {
				int T = QOT.front();
				ofs << QIT[T].front() << endl; /*打印出队的人*/
				if (QIT[T].size() == 1) { QIT[T].pop(); QOT.pop();} /*队首的一队只剩一个人*/
				else QIT[T].pop();
			}
			else  ofs << "操作有误！" << endl; 
		}

	}

	/*关闭文件*/
	ifs.close();
	ofs.close();
	return 0;
}
```

