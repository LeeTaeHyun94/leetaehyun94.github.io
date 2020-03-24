---
layout: post
title:  "[Google Kick Start - Round A 2020] Plates"
description:  "[Google Kick Start - Round A 2020] Plates"
date:   2020-03-23 18:30:00
categories: Algorithm
comments: true
---
[[Google Kick Start - Round A 2020] Plates](https://codingcompetitions.withgoogle.com/kickstart/round/000000000019ffc7/00000000001d40bb)

## 문제 요약

각각 아름다움(1~100)을 나타내는 값을 갖는 K개의 접시가 쌓여 있는 N개의 접시 더미가 있고, 접시는 무조건 더미의 위에서부터 꺼낼 수 있다.  
이 때, 규칙에 맞게 P개의 접시를 꺼내서 최고의 아름다움 값을 구하는 문제

## 풀이

각 접시 더미의 꼭대기에 있는 아름다움 값을 보면서 하나씩 꺼내는 간단한 방법이 바로 떠오르지만, 이는 반례가 있을 수 있다.  
몇 개를 더 꺼냈을 때 아름다움 가치가 더 큰 접시가 있을 가능성을 배제할 수 없기 때문이다.  
그다지 크지 않은 N(1 <= N <= 50), K(1 <= K <= 30), P(1 <= P <= N * K) 범위를 고려해보면 dp[N][P] 형태의 DP 테이블을 생각해 볼 수 있다.  
이 테이블은 N개의 접시더미 안에서 P개의 접시를 꺼냈을 때 구할 수 있는 최고의 아름다움 값을 의미한다.  
누적합 배열을 이용하면 조금 더 편리하게 접시들의 아름다움 값의 합을 구할 수 있다.  

## 코드

```C++
#include <iostream>
#include <algorithm>
using namespace std;
int T, N, K, P, plates[51][31], dp[51][1501];
int main() {
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {
		for (int i = 1; i < 51; i++) {
			for (int j = 1; j < 31; j++) plates[i][j] = 0;
			for (int j = 1; j < 1501; j++) dp[i][j] = 0;
		}
		int ans = 0;
		scanf("%d %d %d", &N, &K, &P);
		for (int i = 1; i <= N; i++)
			for (int j = 1; j <= K; j++) {
				scanf("%d", &plates[i][j]);
				dp[i][j] = dp[i][j - 1] + plates[i][j];
			}
		for (int i = 2; i <= N; i++) {
			for (int j = 1; j <= P; j++) {
				for (int k = 0; k <= j; k++) {
					int sum = 0;
					for (int l = 1; l <= K && l <= j - k; l++) sum += plates[i][l];
					dp[i][j] = max(dp[i][j], dp[i - 1][k] + sum);
				}
			}
		}
		printf("Case #%d: %d\n", tc, dp[N][P]);
	}
	return 0;
}
```