---
layout: post
title:  "Geometry(Convex Hull)"
description: "Computational Geometry(Convex Hull)"
date:   2019-02-26 15:45:00
categories: Algorithm
comments: true
---
- 볼록 외피(Convex Hull) : 주어진 점들을 모두 둘러 싸는 가장 작은 볼록 다각형

- 극단점 (Extreme Point) : 볼록 외피를 구성하는 점을 일컫는다.

- 문제 : 평면 상의 빨간색, 파란색(두 그룹의) 점들이 주어졌을 때, 직선을 그어 평면을 두 영역으로 나눠 각 영역에 같은 색(그룹)의 점만 포함하도록 하는 직선이 존재하는가?

  - 각 그룹의 점들에 대해 그룹 별로 볼록 외피를 구성해본다. 두 볼록 다각형이 겹치거나 닿아 있지 않으면 위 문제에서 설명하는 직선이 존재한다고 할 수 있다.

- 그렇다면 볼록 외피를 어떻게 만들 것인가?

  - 한 극단점을 찾고 그 점에서부터 가장 좌측, 우측에 있는 점들을 찾는 방식이라면 n^2..
  - 조금 더 빠르게는 nlogn

  1. 점들을 x 좌표에 대해 정렬한다.
  2. 정렬한 점들을 통해 순차적으로 다각형을 구성한다.
  3. 구성된 다각형에서 아직 극단점인지 아닌지 알 수 없는 점을 지나는 두 접선을 찾아서 볼록 외피를 늘린다.
     - 그렇다면 접선을 찾는 방법은?
       - 접점이 되는 점을 기준으로 가장 인접한 두 점과 각각 짝을 짓는다.
       - (현재 추가될 점, 접점이 될 가능성이 있는 점, (접점이 될 가능성이 있는 점을 기준으로 가장 인접한 두 점))
       - 위와 같은 점의 쌍들에 대해 CCW 알고리즘을 이용하여 좌 -> 우 또는 우 -> 좌로 방향이 바뀌는 지점이 접점이라고 할 수 있다.
       - 왜냐하면, 바로 직전에 추가된 점은 이전까지 봐왔던 점들의 집합으로 구성된 볼록 외피의 하나의 극단점일 수 밖에 없다. 그렇게 시계 방향과 반시계 방향으로 인접합 세 극단점이 나오지 않을 때 까지 확인해주는 과정을 통해 오목 정점을 제거하고 새로운 볼록 외피를 구성할 수 있다. 이는 재귀적인 상태이기 때문에 항상 정확한 볼록 외피를 구성하며 한 번의 시퀀스동안 나머지 n개의 점들을 모두 확인하지 않기 때문에 nlogn의 시간 복잡도를 갖는다.

```c++
vector<Point> convex_hull(vector<Point> &dat) {
    if (dat.size() < 4) return dat;
    vector<Point> upper, lower;
    sort(dat.begin(), dat.end() [](const Point &a, const Point &b){
        return a.x == b.x ? a.y < b.y : a.x < b.x;
    });
    for (const auto &p : dat) {
        while (upper.size() > 1 && ccw(*++upper.rbegin(), *upper.rbegin(), p) >= 0) upper.pop_back();
        while (lower.size() > 1 && ccw(*++lower.rbegin(), *lower.rbegin(), p) >= 0) lower.pop_back();
        upper.emplace_back(p);
        lower.emplace_back(p);
    }
    upper.insert(upper.end(), ++lower.rbegin(), --lower.rend());
    return upper;
}
```