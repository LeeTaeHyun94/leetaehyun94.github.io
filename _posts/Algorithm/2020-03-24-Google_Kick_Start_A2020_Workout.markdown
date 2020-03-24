---
layout: post
title:  "[Google Kick Start - Round A 2020] Workout"
description:  "[Google Kick Start - Round A 2020] Workout"
date:   2020-03-24 13:34:00
categories: Algorithm
comments: true
---
[[Google Kick Start - Round A 2020] Workout](https://codingcompetitions.withgoogle.com/kickstart/round/000000000019ffc7/00000000001d3f5b)

## 문제 요약

각각 운동 진행 시간을 갖는 N개의 운동 세션과 양의 정수 K가 주어지고, 운동의 어려움 값은 연속된 운동 세션 간의 진행 시간 차이 중 가장 큰 차이이다.  
이 때, K만큼 운동 세션을 추가해서 이 운동의 어려움을 최소로 하고 어려움의 최솟값을 구하는 문제

## 풀이

내가 문제를 해결한 방법은 운동의 어려움 값을 이분탐색으로 늘렸다 줄였다 하면서 해당 어려움 값을 유지하면서 K개의 운동 세션을 추가할 수 있는지 확인하는 작업을 통해 문제를 해결했다.

## 코드

```C++
#include <iostream>
#include <algorithm>
using namespace std;
int T, N, K, arr[100000];
bool go(long long g) {
	int k = K, pre = arr[0];
	for (int i = 1; i < N; i++) {
		int gap = arr[i] - pre - 1;
		if (gap > 0) k -= gap / g;
		pre = arr[i];
		if (k < 0) return 1;
	}
	return 0;
}
int main() {
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {
		long long l = 1, r = 0;
		scanf("%d %d", &N, &K);
		for (int i = 0; i < N; i++) {
			scanf("%d", &arr[i]);
			if (i > 0) r = max(r, (long long)arr[i] - arr[i - 1]);
		}
		while (l <= r) {
			long long m = (l + r) / 2;
			go(m) ? l = m + 1 : r = m - 1;
		}
		printf("Case #%d: %lld\n", tc, l);
	}
	return 0;
}
```