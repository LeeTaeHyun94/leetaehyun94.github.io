---
layout: post
title:  "[Algospot] FESTIVAL - 록 페스티벌"
description:  "[Algospot] FESTIVAL - 록 페스티벌"
date:   2019-08-27 23:40:00
categories: Algorithm
comments: true
---
[[Algospot] FESTIVAL](https://algospot.com/judge/problem/read/FESTIVAL)

최근에 종만북을 다시보며 10달 전에 풀었었던 문제를 다시 풀기 시작했다. 첫 장에 나오는 문제라 쉬운 편이었지만, 오랜만의 문제 풀이라 앞으로 더 힘들어질 것 같다.

## 문제 요약

L개의 밴드가 있어 하루에 하나의 밴드가 공연을 할 수 있다고 하면, 페스티벌을 최소 L일 이상 진행해야 한다. 그 때, N일 동안의 공연장 대여 비용이 주어지고, 이 중 L일 이상을 연속해서 대여하되, 공연장을 빌리는데 드는 평균 비용을 최소화하는 문제

## 풀이

가장 쉽게 떠올릴 수 있는 방법은 i(0 <= i <= N - L) ~ j(L <= j <= N)의 범위를 모두 탐색하여 평균 값을 비교하는 방법이다. 하지만, 이 방법은 최악의 경우, O(N^3)의 시간복잡도가 될 수 있기 때문에 조금의 최적화가 더 필요하다.  
또한, 주어진 시간 제한과 C, N, L의 범위를 고려했을 때,  O(N^2)의 시간복잡도 정도는 허용됨을 알 수 있다.
L일 이상 연속해서 대여한다는 사실에서 약간의 힌트(?)를 얻을 수 있는데, 평균이라는 것은 비용의 합들을 개수로 나누어 주는 것이기 때문에 비용의 합 자체를 연속합 배열을 미리 구성해놓고 인덱스를 빼는 것으로 구하면 시간복잡도를 O(N^2)으로 줄일 수 있다.

## 코드

```C++
#include<cstdio>
#include<algorithm>
using namespace std;
int C, N, L, n[1001];
int main() {
	for (scanf("%d", &C); C--;) {
		scanf("%d %d", &N, &L);
		for (int i = 1; i <= N; i++) scanf("%d", &n[i]), n[i] += n[i - 1];
		double ans = 1e9;
		for (int i = 0; i <= N - L; i++)
			for (int j = i + L; j <= N; j++)
				ans = min(ans, double(n[j] - n[i]) / (j - i));
		printf("%.11f\n", ans);
	}
	return 0;
}
```