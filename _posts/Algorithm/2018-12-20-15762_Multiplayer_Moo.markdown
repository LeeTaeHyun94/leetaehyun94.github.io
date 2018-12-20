---
layout: post
title:  "[BOJ 15762] Multiplayer Moo"
date:   2018-12-20 21:00:00
categories: Algorithm
comments: true
---
[[BOJ 15762] Multiplayer Moo](https://www.acmicpc.net/problem/15762)

오늘 포스팅하는 문제는 며칠 전부터 코딩에 대한 아이디어 때문에 굉장히 고민을 오래한 문제이다.

이전의 USACO 문제들을 조금 풀어봤었지만 여태 푼 Silver 문제들 중 가장 어려웠던 것 같다......

그동안 멘탈 와르르맨션이어서.. 너무 알고리즘을 안 했던 탓일까..

앞으로는 더 열심히, 꾸준히 해야겠다!

## 문제 요약

게임판이 주어지고 게임판에는 0~1000000 사이 범위의 숫자로 영역이 표시된다.

하나의 숫자로 이루어진 가장 큰 영역과 두 개의 숫자로 이루어진 가장 큰 영역을 구하는 문제.

## 풀이

언뜻 보면 간단해 보이지만 주어지는 N의 범위가 250이다. 처음에는 하던대로 BFS를 통해 가장 큰 영역의 크기를 구해주면 되겠거니 하고 코딩하던 중 해법을 조금 더 생각해봐야 겠다고 깨달았다.

1. 무작정 BFS를 한다면 두 개의 숫자로 이루어진 영역은 어떻게..? 라는 의문이 생긴다.
2. 첫 번째 BFS를 통해 각 영역별로 다시 labeling하는 작업 이후에 그래프를 재구성한다면?
3. 나올 수 있는 두 개의 숫자 모든 조합에 대해서 재구성된 그래프를 계속해서 탐색해주어야 한다.
   - 이렇게 되면 최악의 경우 N^4, 주어진 시간 내에 해결하지 못한다.
4. 그렇다면 그래프를 조금 더 최소화해서 재구성해야 한다.

이 순서대로 차근차근 생각이 들었고 마지막으로 결론 지을 수 있던 것은 재구성할 그래프가 꼭 전부 다 필요하지 않다는 점이었다.

다시 말해서, 두 개의 숫자 조합을 지키며 인접해 있는 부분들에 대해서만 연결한다면, 조합에 따라 필요한 부분만 탐색하게 되고 모든 영역이 다 연결되게 된다고 해도 가능한 숫자 조합은 단 한가지가 되기 때문에, 결국 모든 그래프를 탐색하는 작업은 합쳐서 단 한 번이라는 것이다.

이렇게 해법을 찾았지만, 구현 능력에 가로막혀 시간이 오래 걸렸다.

구현 문제를 더 많이 풀어봐야 겠다는 생각이 많이 드는 문제였다...

## 코드

```C++
#include<iostream>
#include<queue>
#include<set>
#include<map>
#include<algorithm>
using namespace std;
int N, b[250][250], C[250][250], val[62501], oc[62501], c, cnt, ans1, ans2, dx[] = { 1,0,-1,0 }, dy[] = { 0,1,0,-1 };
map<pair<int, int>, map<int, pair<bool, set<int>>>> m;

void go(int p1, int p2, int c1, int c2) {
	if (p1 > p2) swap(p1, p2);
	auto p = make_pair(p1, p2);
	m[p][c1].second.insert(c2);
	m[p][c2].second.insert(c1);
}

int main() {
	scanf("%d", &N);
	for (int i = 0; i < N; i++) for (int j = 0; j < N; j++) scanf("%d", &b[i][j]);
	for (int i = 0; i < N; i++)
		for (int j = 0; j < N; j++) {
			queue<pair<int, int>> q;
			if (!C[i][j]) {
				cnt = 1;
				q.push({ j, i });
				C[i][j] = ++c;
				val[c] = b[i][j];
				while (q.size()) {
					int x = q.front().first, y = q.front().second;
					q.pop();
					for (int k = 0; k < 4; k++) {
						int nx = x + dx[k], ny = y + dy[k];
						if (0 <= nx && nx < N && 0 <= ny && ny < N && b[y][x] == b[ny][nx] && !C[ny][nx]) {
							C[ny][nx] = c;
							cnt++;
							q.push({ nx,ny });
						}
					}
				}
				oc[c] = cnt;
				ans1 = max(ans1, cnt);
			}
		}
	for (int i = 0; i < N; i++)
		for (int j = 0; j < N; j++) {
			if (i < N - 1 && C[i][j] != C[i + 1][j]) go(b[i][j], b[i + 1][j], C[i][j], C[i + 1][j]);
			if (j < N - 1 && C[i][j] != C[i][j + 1]) go(b[i][j], b[i][j + 1], C[i][j], C[i][j + 1]);
		}
	for (auto p1 : m) {
		for (auto p2 : p1.second) {
			if (!p2.second.first) {
				queue<int> q;
				auto p = p1.first;
				int n = p2.first;
				q.push(n);
				cnt = oc[n];
				m[p][n].first = 1;
				while (q.size()) {
					int u = q.front();
					q.pop();
					for (int v : m[p][u].second) {
						if (m[p][v].first) continue;
						m[p][v].first = 1;
						cnt += oc[v];
						q.push(v);
					}
				}
			}
			ans2 = max(ans2, cnt);
		}
	}
	printf("%d\n%d", ans1, ans2);
	return 0;
}
```