---
layout: post
title:  "[Google Kick Start - Round A 2020] Allocation"
description:  "[Google Kick Start - Round A 2020] Allocation"
date:   2020-03-22 18:30:00
categories: Algorithm
comments: true
---
[[Google Kick Start - Round A 2020] Allocation](https://codingcompetitions.withgoogle.com/kickstart/round/000000000019ffc7/00000000001d3f56)

## 문제 요약

가격이 정해져 있는 N개의 집이 존재하고 B 달러를 소유하고 있다고 할 때, 가지고 있는 돈으로 살 수 있는 최대한 많은 집의 수를 구하는 문제

## 풀이

정해진 돈으로 집을 최대한 많이 사려면 그리디하게 가격이 싼 집을 골라서 사야 한다.  

## 코드

```C++
#include <iostream>
#include <algorithm>
using namespace std;
int T, N, B, A[100000];
int main() {
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {
		int ans = 0;
		scanf("%d %d", &N, &B);
		for (int i = 0; i < N; i++) scanf("%d", &A[i]);
		sort(A, A + N);
		for (int i = 0; i < N; i++) {
			if (B < A[i]) break;
			B -= A[i];
			ans++;
		}
		printf("Case #%d: %d\n", tc, ans);
	}
	return 0;
}
```