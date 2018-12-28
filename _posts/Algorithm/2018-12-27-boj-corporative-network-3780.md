---
layout: post
title: BOJ - 네트워크 연결(3789)
category: Algorithm
tag: [BOJ, 백준, 알고리즘, 자료구조]
---

**Disjoint Set** 문제이며 **유니온 파인드(Union-Find)**를 사용해서 해결할 수 있는 문제입니다. 중요한 부분은 find를 할 때 기존 경로 압축(path compression)을 하면서 거리도 업데이트 해줘야 합니다. merge 할 때는 최상위 노드를 따로 찾을 필요 없이 입력으로 들어온 두 노드를 바로 연결 해주면 됩니다. 

<div class="message">
경로 압축(path compression)을 하지 않고, 매번 재귀로 거리를 계산하면 Timeout이 발생합니다.
</div>

## 라인 길이
```
// define
#define MAX 200010

// distance to center
int dist[MAX];

// get distance
int distance(int a, int b) {
	int dist = a > b ? a - b : b - a;
	return dist % 1000;
}
```


## 유니온 파인드
```
int parent[MAX];

int find(int n) {
	if (parent[n] == 0) return n;
	int p = find(parent[n]);

	//// 길이 업데이트 ////
	dist[n] += dist[parent[n]];
	
	parent[n] = p;
	return p;
	
}

void merge(int a, int b) {
	dist[a] = distance(a, b);
	parent[a] = b;
}
```

## 메인 함수
```
#include <stdio.h>
int main() {

	int T;
	scanf("%d", &T);

	while(T--) {
		// initialize
		for (int i = 0; i < MAX; i++) {
			dist[i] = 0;
			parent[i] = 0;
		}

		int N;
		scanf("%d", &N);
		while(true) {

			char command;
			scanf(" %c", &command);
			if (command == 'O') {
				break;
			}

			if (command == 'E') {
				int i;
				scanf("%d", &i);
				find(i);
				printf("%d\n", dist[i]);
			} else {
				int i, j;
				scanf("%d %d", &i, &j);
				merge(i, j);
			};
		}
	}
	return 0;
}
```