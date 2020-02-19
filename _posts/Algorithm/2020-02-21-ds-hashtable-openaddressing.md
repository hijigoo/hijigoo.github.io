---
layout: post
title: 자료구조 - 해시테이블 (open addressing)
category: Algorithm
tag: [알고리즘, 자료구조]
---

알고리즘을 풀다보면 해시테이블 구현에 익숙해져야 합니다. 이번에는 구현이 쉬운 **open addressing**을 이용한 해시테이블을 구현해보았습니다. 처음에는 int 자료형을 다루는 코드고, 이어서 구조체를 다루는 코드입니다. 모두 구현에 필요한 핵심은 같습니다.

<div class="message">
주의 사항으로, 데이터를 삭제할 때는 빈값을 넣는 것이 아니라 더미 값을 넣어서 삭제되었다는 것을 표시해주어야 합니다. 그렇지 않으면 해시테이블에서 데이터를 검색할 때 끝까지 검색하지 않고 중간에 끊길 수 있습니다. 
</div>

## int 자료형을 다루는 해시테이블
```
#include <iostream>
using namespace std;

#define MAX_HASH_SIZE 100017

int hash_map[MAX_HASH_SIZE];

// 비어 있거나 삭제된 위치에 넣을 수 있다.
void insert(int data) {
	int hash_idx = data % MAX_HASH_SIZE;
	while (hash_map[hash_idx] != 0 && hash_map[hash_idx] != -1) {
		hash_idx = ++hash_idx % MAX_HASH_SIZE;
	}
	hash_map[hash_idx] = data;
}

// 비어 있을 때까지 검색한다.
int find(int data) {
	int hash_idx = data % MAX_HASH_SIZE;
	while (hash_map[hash_idx] != 0) {
		if (hash_map[hash_idx] == data) {
			return hash_map[hash_idx];
		}
		hash_idx = ++hash_idx % MAX_HASH_SIZE;
	}
	return -1;
}

// 위치를 찾아서 -1 로 마킹한다.
int remove(int data) {
	int hash_idx = data % MAX_HASH_SIZE;
	if (hash_map[hash_idx] != 0) {
		if (hash_map[hash_idx] == data) {
			int find = hash_map[hash_idx];
			hash_map[hash_idx] = -1;
			return find;
		}
		hash_idx = ++hash_idx % MAX_HASH_SIZE;
	}
	return false;
}

int main() {

	insert(4);
	insert(6);
	insert(15);
	insert(9);
	insert(19);

	printf("%d\n", find(4));
	printf("%d\n", remove(15));
	printf("%d\n", find(15));

	insert(15);
	printf("%d\n", find(15));
	printf("%d\n", find(9));

	return 0;
}
```

## 구조체를 다루는 해시테이블
```
#include <stdio.h>
using namespace std;

#define MAX_HASH_SIZE 100017
#define MAX_NODE 50000

struct Node {
	int hash;
	int key;
} node_arr[MAX_NODE];

int node_arr_idx = 0;
Node* get_node(int key) {
	Node* node = &node_arr[node_arr_idx++];
	node->key = key;
	node->hash = key % MAX_HASH_SIZE;
	return node;
}

Node* hash_arr[MAX_HASH_SIZE];
Node* dummy = get_node(-1);

void insert(Node* node) {
	int hash_idx = node->hash;
	while (hash_arr[hash_idx] != 0 && hash_arr[hash_idx]->key != -1) {
		hash_idx++;
		hash_idx = hash_idx % MAX_HASH_SIZE;
	}
	hash_arr[hash_idx] = node;
}

Node* find(int key) {
	int hash_idx = key % MAX_HASH_SIZE;
	while (hash_arr[hash_idx] != 0) {
		if (hash_arr[hash_idx]->key == key) {
			return hash_arr[hash_idx];
		}
		hash_idx++;
		hash_idx = hash_idx % MAX_HASH_SIZE;
	}
	return 0;
}

Node* remove(int key) {
	int hash_idx = key % MAX_HASH_SIZE;
	while (hash_arr[hash_idx] != 0) {
		if (hash_arr[hash_idx]->key == key) {
			Node* find = hash_arr[hash_idx];
			hash_arr[hash_idx] = dummy;
			return find;
		}
		hash_idx++;
		hash_idx = hash_idx % MAX_HASH_SIZE;
	}
	return 0;
}

int main() {


	return 0;
}
```