---
layout: post
title:  "[Google Kick Start - Round E] Cherries Mesh"
description:  "[Google Kick Start - Round E] Cherries Mesh"
date:   2019-08-30 18:30:00
categories: Algorithm
comments: true
---
[[Google Kick Start - Round E] Cherries Mesh](https://codingcompetitions.withgoogle.com/kickstart/round/0000000000050edb/0000000000170721)

## 문제 요약

Cherries Mesh라는 디저트를 만들었는데, 설탕 함량이 너무 높다. 이 디저트는 N(1 ~ N) 개의 체리가 당도가 1인 검정색 또는 당도가 2인 빨간색의 설탕 끈(?)으로 각각 서로 연결되어 있다.  
입력으로는 검은색 설탕 끈에 대한 정보가 주어지는데, 나머지 설탕 끈은 빨간색이라고 한다.
이 때, 모든 체리들이 연결되어 있는 것을 유지하며, 최대한 설탕 끈을 제거하여 최소의 당도를 구하는 문제

## 풀이

가장 먼저 떠올려야 하는 것은 모든 체리들의 연결을 유지하며, 최대한 설탕 끈을 제거한다는 점에서 시작된다. 체리를 정점, 설탕 끈을 간선으로 생각해보면, 간선의 개수가 정점 개수보다 하나 작다는 최소 신장 트리의 특징이 떠오른다.  
두 번째로 떠올려야 하는 것은 설탕 끈을 간선으로 생각했을 때, 당도를 가중치라고 생각할 수 있고, 이는 가중치가 1 또는 2 둘 밖에 없음을 알 수 있다. 때문에 입력으로 주어지는 검정색 설탕 끈을 최대한으로 이용해야만 최소의 당도를 구할 수 있다.  
  
Union-Find를 활용하여 검정색 설탕 끈으로 연결할 수 있는 체리들을 최대한 연결하여 하나 이상의 컴포넌트로 구성해준 다음, 나머지 부족한 설탕 끈은 빨간색으로 연결한다고 생각해서 (컴포넌트의 개수 - 1) * 2의 당도를 더해주면 된다.


## 코드

```C++
#include<cstdio>
int T, N, M, c[100001];

int find(int x) {
	if (c[x] < 0) return x;
	return c[x] = find(c[x]);
}

bool merge(int x, int y) {
	x = find(x);
	y = find(y);
	if (x == y) return false;
	c[y] = x;
	c[x]--;
	return true;
}

int main() {
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {
		for (int i = 1; i <= 1e5; i++) c[i] = -1;
		int ans = 0, cnt = 0;
		scanf("%d %d", &N, &M);
		for (int i = 0, C, D; i < M; i++) {
			scanf("%d %d", &C, &D);
			if (merge(C, D)) ans++;
		}
		for (int i = 1; i <= N; i++)
			if (c[i] < 0) cnt++;
		ans += (cnt - 1) * 2;
		printf("Case #%d: %d\n", tc, ans);
	}
	return 0;
}
```