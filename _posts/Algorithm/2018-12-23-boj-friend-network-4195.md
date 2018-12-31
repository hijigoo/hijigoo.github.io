---
layout: post
title: BOJ - 친구 네트워크(4195)
category: Algorithm
tag: [BOJ, 백준, 알고리즘, 자료구조]
---

**유니온 파인드(Union-Find)**를 사용해서 해결할 수 있는 문제입니다. 그런데 find 과정에서 단순하게 문자열 비교를 하면 Timeout이 발생합니다. 이를 해결하기 위해서 문자열을 **hash code**로 변환해서 비교해야 합니다. **HashMap**을 만들 때 hash code가 겹칠 수 있기 때문에 **Linked List**를 사용했습니다. 이런 방식을 [**Separate chaining**](https://en.wikipedia.org/wiki/Hash_table#Separate_chaining)이라고 합니다. 기존의 HashMap 라이브러리를 사용하셔도 됩니다. 

hash code 구하는 식은 [Naver D2](https://d2.naver.com/helloworld/831311)를 참고했습니다. 

<div class="message">
문자열을 배열로 받으면 주소가 고정되어서, Node에 저장된 name이 다음 입력을 받을 때 변경되는 문제가 있었습니다. 이 문제를 해결하고자 문자열을 동적 할당해서 매번 다른 주소값에 맵핑 되도록 수정했습니다. 문자열을 카피해서 해결하는 방법도 있습니다.
</div>



## 노드
```
// define
#define MAX 200010

// node
struct Node {
	Node* next;
	int idx;
	char* name;
}nodearr[MAX];

int nodeidx = 0;
Node* allocnode(char* name, int idx) {
	Node* node = &nodearr[nodeidx++];
	node->name = name;
	node->idx = idx;
	return node;
}
```

## Hash Code 
```cpp
int hashCode(char* str) {
	int hash = 0;
	for (int i = 0; str[i] != '\0'; i++) {
		hash = (hash * 31 + str[i]) % MAX;
	}
	return hash;
}
```

## Hash Map
```
Node* h[MAX];

int get(char* name) {
	int hash = hashCode(name);

	Node* cur = h[hash];
	while (cur != '\0') {
		int isSame = 1;
		for (int i = 0; i < 21; i++) {
			if (name[i] != cur->name[i]) {
				isSame = 0;
				break;
			}
		}
		if (isSame) return cur->idx;
		cur = cur->next;
	}
}

void put(char* name, int idx) {
	int hash = hashCode(name);
	Node* node = allocnode(name, idx);
	if (h[hash] == '\0') h[hash] = node;
	else {
		node->next = h[hash];
		h[hash] = node;
	}
}

int isContain(char* name) {
	int hash = hashCode(name);
	if (h[hash] == '\0') return 0;
	else {
		Node* cur = h[hash];
		while (cur != '\0') {
			int isSame = 1;
			for (int i = 0; i < 21; i++) {
				if (name[i] != cur->name[i]) {
					isSame = 0;
					break;
				}
			}
			if (isSame) return 1;
			cur = cur->next;
		}
		return 0;
	}
}
```

## 유니온 파인드
```
int find(int n) {
	if (p[n] < 0) return n;
	else {
		// path compression
		p[n] = find(p[n]);
		return p[n];
	}
}

int uni(int a, int b) {

	int ap = find(a);
	int bp = find(b);

	if (ap != bp) {
		p[bp] = ap;
		c[ap] += c[bp];
	}

	return c[ap];
}
```

## 메인 함수
```
#include <stdio.h>
#include <stdlib.h>
int main() {

	int T;
	scanf("%d", &T);

	while (T--) {
		int nameCount = 1;
		for (int i = 0; i < MAX; i++) {
			p[i] = -1;
			c[i] = 1;
		}

		int F;
		scanf("%d", &F);

		while (F--) {

			char* a = (char*)malloc(sizeof(char) * 21);
			char* b = (char*)malloc(sizeof(char) * 21);

			scanf("%s", a);
			scanf("%s", b);

			if (isContain(a) == 0) {
				put(a, nameCount++);
			}
			if (isContain(b) == 0) {
				put(b, nameCount++);
			}

			int count = uni(get(a), get(b));
			printf("%d\n", count);
		}

	}

	return 0;
}
```