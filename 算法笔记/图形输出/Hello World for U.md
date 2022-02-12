

```c++
#include<cstdio>
#include<cstring>

int main() {

	char s[85];
	scanf("%s", s);
	int len = strlen(s);
	int side = (len + 2) / 3; /*两边长*/
	int mid = len + 2 - side * 2;/*中间长*/

	for (int i = 0; i < side - 1; i++) {
		putchar(s[i]);
		for (int j = 0; j < mid-2; j++) putchar(' ');
		printf("%c\n", s[len - 1 - i]);
	}
	for (int i = side - 1; i < side - 1 + mid; i++) putchar(s[i]);
	
	
	return 0;
}
```

