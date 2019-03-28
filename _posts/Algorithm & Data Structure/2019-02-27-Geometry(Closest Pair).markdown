---
layout: post
title:  "Geometry(Closest Pair)"
description: "Computational Geometry(Closest Pair)"
date:   2019-02-27 15:45:00
categories: Algorithm
comments: true
---
- 평면 상에 N개의 점들이 주어졌을 때, 가장 가까운 두 점을 찾아라.
  - Naive algorithm = O(N^2)

  - Divide & Conquer
    - N개 점들의 집합 S를 N/2개 씩 각각 집합 S1, S2로 나눈다. (점들의 x좌표의 중간 값(median)을 이용)
    - 집합 안에서 최근접쌍 문제를 해결
    - 집합을 합치면서 S1의 한 점과 S2의 한 점을 쌍을 이뤄보면서 서로 다른 집합에서 최근접쌍이 나오는지를 검사한다. 이 때 비교하는 영역에 대해 자명한 사실에 의해 한정 지어주게 되면 빠르게 검사할 수 있다. 추가적으로 이 때, merge sort algorithm에서 해줬던 것처럼 병합까지 해준다면 정렬된 집합을 병합했기 때문에 추가적으로 정렬이 필요하지 않게 되므로 Nlog^2N에서 NlogN으로 줄일 수 있다.
      - ![Closest Pair 1](../../assets/Algorithm/14.PNG)
      - ![Closest Pair 2](../../assets/Algorithm/15.PNG)
      - ![Closest Pair 3](../../assets/Algorithm/16.PNG)
      - ![Closest Pair 4](../../assets/Algorithm/17.PNG)
      - ![Closest Pair 5](../../assets/Algorithm/18.PNG)
    - 위 세 가지 시퀀스를 재귀적으로 반복하게 된다면? 적어도 점 두 개가 포함되어 있는 최소 크기의 집합까지 내려갔다가 올라오면서 보다 빠르게 nlogn 시간에 최근접쌍을 구할 수 있다.
    - 출처 : http://swexpertacademy.com


  - Line Sweeping

    - 라인 스위핑 기법 또한 위에서 기술된 아이디어에서 집합을 반으로 나누는 부분을 제외한 아이디어를 기반으로 작동한다.

    - ```C++
      int n;
      set<pair<int, int>> s;
      pair<int, int> N[100000];
      
      int main() {
      	scanf("%d", &n);
      	for (int i = 0; i < n; i++) scanf("%d %d", &N[i].x, &N[i].y);
      	sort(N, N + n);
      	int ans = 2e9;
      	for (int i = 0, idx = 0; i < n; i++) {
      		int d = sqrt(ans);
      		while (N[i].x - N[idx].x > d) s.erase({ N[idx].y, N[idx++].x });
      		for (auto j = s.lower_bound({ N[i].y - d, -10000 }); j != s.end() && j->x <= N[i].y + d; j++)
      			ans = min(ans, (N[i].x - j->y) * (N[i].x - j->y) + (N[i].y - j->x) * (N[i].y - j->x));
      		s.insert({ N[i].y,N[i].x });
      	}
      	printf("%d\n", ans);
      	return 0;
      }
      ```