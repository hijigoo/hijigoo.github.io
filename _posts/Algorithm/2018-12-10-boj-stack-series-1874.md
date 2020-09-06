---
layout: post
title: BOJ - 스택 수열(1874)
category: Algorithm
tag: [BOJ, 백준, 알고리즘, 자료구조]
---

구조체 배열이 아닌 단순 **배열**을 사용해서 구현한 스택 수열 알고리즘 코드입니다.




## 배열과 헤드위치 선언
```cpp
int stack[100005];
int head = 0;
```


## 전체 코드

```cpp
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

		// 수열이 형성되지 못하는 경우 체크
		if (head < 0 || number < stack[head]) {
			isFailed = true;
			break;;
		}

		// 출력(POP)되어야 할 숫자(number)가 스택에 들어갈 때까지 PUSH
		while (stack[head] < number) {
			output[outputIdx++] = '+';
			stack[++head] = inc;
			inc++;
		}
		
		// 숫자(number)를 출력(POP)
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