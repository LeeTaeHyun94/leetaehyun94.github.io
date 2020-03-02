---
layout: post
title:  "[Google Kick Start - Round E] Code-Eat Switcher"
description:  "[Google Kick Start - Round E] Code-Eat Switcher"
date:   2019-09-01 18:30:00
categories: Algorithm
comments: true
---
[[Google Kick Start - Round E] Code-Eat Switcher](https://codingcompetitions.withgoogle.com/kickstart/round/0000000000050edb/00000000001707b8)

## 문제 요약

하루에 코딩 혹은 식사를 할 수 있는데, 코딩 양과 식사량이 하나의 루틴으로 주어지고, 이 루틴은 여러 개가 있다. 이 때, 쿼리로 코딩 목표치와 식사 목표치가 주어지고 여러 날동안 루틴을 적절한 비율로 수행하여 목표로 하는 코딩 양과 식사량을 달성할 수 있는지 알아내는 문제

## 풀이

내가 문제를 해결한 방법은 그리디한 방법이다.  
주어진 모든 날에 대해 100% 코딩에만 집중했다고 가정했을 때, 그 코딩 양보다 많은 목표치는 달성할 수 없다는 것을 알 수 있다.  
그리고 코딩 양에 비해 식사량이 많은 루틴에서부터 목표치보다 초과 달성한 코딩 양만큼 코딩을 안 하고 식사를 한다고 생각해보자. 이것이 가장 효율적으로 코딩 양과 식사량을 분배하는 방법 중 하나라는 사실을 깨달아야 한다.  
다시 말해, 코딩 양은 목표치에 정확히 맞춰두고 여유 분의 코딩 양만큼 식사를 진행한다는 것이다. 이렇게 계산하고 난 뒤, 식사량이 목표치에 도달하지 못한다면 그 목표는 달성할 수 없다.  
때문에 코딩 양에 비해 식사량이 많은 루틴부터 내림차순으로 루틴을 정렬하고, 코딩 양이 많은 목표 날짜부터 내림차순으로 쿼리를 정렬한 다음, 차례대로 순서에 맞게 여부만 결정해주면 된다.

## 코드

```C++
#include<iostream>
#include<algorithm>
#include<cmath>
using namespace std;
int T, D, S;
char ans[100001];
pair<double, double> CE[100000];
pair<pair<double, double>, int> AB[100000];
int main() {
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {
		scanf("%d %d", &D, &S);
		double cs = 0, es = 0, dc = 0;
		for (int i = 0; i < S; i++) scanf("%lf %lf", &CE[i].first, &CE[i].second), cs += CE[i].first;
		for (int i = 0; i < D; i++) scanf("%lf %lf", &AB[i].first.first, &AB[i].first.second), AB[i].second = i;
		sort(CE, CE + S, [](pair<double, double> &A, pair<double, double> &B) {
			return A.second / A.first > B.second / B.first;
		});
		sort(AB, AB + D);
		for (int i = D - 1, j = 0; i >= 0; i--) {
			if (cs < AB[i].first.first) {
				ans[AB[i].second] = 'N';
				continue;
			}
			double rc = cs - AB[i].first.first;
			while (j < S && rc) {
				double change = min(rc, CE[j].first - dc);
				rc -= change;
				cs -= change;
				es += change / CE[j].first * CE[j].second;
				if (rc) dc = 0, j++;
				else {
					dc += change;
					break;
				}
			}
			if (es >= AB[i].first.second) ans[AB[i].second] = 'Y';
			else ans[AB[i].second] = 'N';
		}
		printf("Case #%d: ", tc);
		for (int i = 0; i < D; i++) printf("%c", ans[i]);
		puts("");
	}
	return 0;
}
```