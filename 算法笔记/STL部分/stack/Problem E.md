



```c++
#include<iostream>
#include<string>
#include<stack>
using namespace std;

int main() {
	int n;
	cin >> n;
    while (n--) {
        string s;
        stack<char> st;
        cin >> s;
        bool flag = true;
        for (auto it = s.begin(); it != s.end(); it++) {
            if (*it == '(' || *it == '[' || *it == '{') st.push(*it);
            else if (*it == ')') {
                if (st.size() > 0 && st.top() == '(') st.pop();
                else { flag = false; break; }
            }
            else if (*it == ']') {
                if (st.size() > 0 && st.top() == '[') st.pop();
                else { flag = false; break; }
            }
            else if (*it == '}') {
                if (st.size() > 0 && st.top() == '{') st.pop();
                else { flag = false; break; }
            }
        }
        if (flag && st.empty()) cout << "yes" << endl;
        else cout << "no" << endl;
    }

	return 0;
}
```

