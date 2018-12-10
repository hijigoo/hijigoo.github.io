---
layout: post
title: 백준 알고리즘 - 스택 수열(1874)
category: Algorithm
tag: [백준, 알고리즘, 자료구조]
---

구조체 배열이 아닌 단순 **배열**을 사용해서 구현한 스택 수열 알고리즘 코드입니다.




## 단순한 스택을 위한 배열과 헤드위치 선언
```
int stack[100005];
int head = 0;
```


## 전체 코드

```
#include <stdio.h>

int stack[100005];
int head = 0;

int main() {

	int n;
	scanf("%d", &n);

	int inc = 1;

	int outputIdx = 0;
	char output[500005];
	bool isFailed = false;

	while(n--) {

		int number;
		scanf("%d", &number);

		if (head < 0 || number < stack[head]) {
			isFailed = true;
			break;;
		}

		while (stack[head] < number) {
			output[outputIdx++] = '+';
			stack[++head] = inc;
			inc++;
		}

		while (stack[head] >= number) {
			output[outputIdx++] = '-';
			head--;
		}

	}

	if (isFailed) {
		printf("NO\n");
	} else {
		for (int i = 0; i < outputIdx; i++ ) {
			printf("%c\n", output[i]);
		}
	}
	return 0;
}
```