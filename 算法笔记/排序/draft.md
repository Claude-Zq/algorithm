# 插入排序



```c++
void InsertSort(int a[], int n) {

	for (int i = 1; i < n; i++) {
		int temp = a[i], j = i;//可以把j理解为空位的索引
		while (j >= 1 && temp < a[j-1]) { a[j] = a[j - 1]; j--; }
		a[j] = temp;
	}
}
```

