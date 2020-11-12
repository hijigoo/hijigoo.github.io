---
layout: post
title: 탐색 - Trie Wildcard 
category: Algorithm
tag: [알고리즘, 탐색]
---

Wildcard(*)가 포함된 단어 찾기 입니다. *는 0개 이상의 알파벳으로 대체될 수 있습니다. 단어를 빠르게 찾는 방법으로 Trie를 사용했습니다.

Search를 할 때 아래 3가지 경우로 나눠서 재귀로 검색했습니다.

1. Wildcard(*) 가 아닌 경우
2. Wildcard(*) 가 0개의 알파벳을 의미하는 경우
3. Wildcard(*) 가 1개의 알파벳을 의미하는 경우 


## Trie 구현
```cpp
#define MAX_TRIE 5000

// 정의
struct Trie;
Trie* get_empty_trie();

// Trie 구현
struct Trie {
	Trie* child[26];
	int count;

	void add_word(const char* word, int index) {
		if (word[index] == 0) {
			count++;
			return;
		}

		int id = (word[index] - 'a');
		if (child[id] == 0) {
			child[id] = get_empty_trie();
		}

		child[id]->add_word(word, index + 1);
	}

	int count_word(const char* word, int index) {

		if (word[index] == 0) {
			return count;
		}

		int ret = 0;
		
		// wildcard 가 아닌 경우 다음 탐색
		if (word[index] != '*') {
			int id = (word[index] - 'a');
			if (child[id] != 0) {
				return child[id]->count_word(word, index + 1);
			}
			return 0;
		}

		// wildcard 인 경우 모두 탐색
		if (word[index] == '*') {
			// *가 0개의 알파벳을 의미하는 경우
			ret += count_word(word, index + 1);

			// *가 1개의 알파벳을 의미하는 경우
			for (int i = 0; i < 26; i++) {
				if (child[i] != 0) {
					ret += child[i]->count_word(word, index);
				}
			}
			return ret;
		}

		return ret;
	}

};

// Trie 초기화 및 가져오기 
Trie trie_arr[MAX_TRIE];
int trie_arr_idx;
Trie* get_empty_trie() {
	Trie* ret = &trie_arr[trie_arr_idx++];
	ret->count = 0;
	for (int i = 0; i < 26; i++) {
		ret->child[i] = 0;
	}
	return ret;
}
```

## 테스트
```cpp
#include <stdio.h>
using namespace std;

int main() {
	trie_arr_idx = 0;
	Trie* root = get_empty_trie();
	
	// 삽입
	root->add_word("abc", 0);
	root->add_word("abcdef", 0);
	root->add_word("abcd", 0);
	root->add_word("abc", 0);

	// 검색
	printf("%d\n", root->count_word("abc*", 0)); // 4
	printf("%d\n", root->count_word("*abc", 0)); // 2
	printf("%d\n", root->count_word("a*c", 0)); // 2
	printf("%d\n", root->count_word("a*d", 0)); // 1
	printf("%d\n", root->count_word("a*ef", 0)); // 1
	printf("%d\n", root->count_word("abcdef*", 0)); // 1
	printf("%d\n", root->count_word("*abcdef", 0)); // 1
	printf("%d\n", root->count_word("a*", 0)); // 4
	printf("%d\n", root->count_word("*e", 0)); // 0
	printf("%d\n", root->count_word("e*", 0)); // 0
	printf("%d\n", root->count_word("*ab", 0)); // 0

	return 0;
}
```

## 출력
```
4
2
2
1
1
1
1
4
0
0
0
```