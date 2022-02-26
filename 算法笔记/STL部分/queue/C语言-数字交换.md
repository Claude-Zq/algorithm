






```c++
#include<cstdio>

const int num = 10;
int main() {
    
    int a[num];
    for (int i = 0; i < num; i++) scanf("%d", &a[i]);

    int minPos = 0;
    for (int i = 1; i < num; i++) if (a[i] < a[minPos]) minPos = i;
    if (minPos != 0) {
        int temp = a[minPos];
        a[minPos] = a[0];
        a[0] = temp;
    }

    int maxPos = 0;
    for (int i = 1; i < num; i++) if (a[i] > a[maxPos]) maxPos = i;
    if (maxPos != 0) {
        int temp = a[maxPos];
        a[maxPos] = a[num-1];
        a[num-1] = temp;
    }
    for (int i = 0; i < num; i++) printf("%d ", a[i]);
    return 0;
}  
```
