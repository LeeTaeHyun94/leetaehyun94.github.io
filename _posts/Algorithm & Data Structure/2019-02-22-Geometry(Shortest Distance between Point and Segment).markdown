---
layout: post
title:  "Geometry(Shortest Distance between Point and Segment)"
description: "Computational Geometry(Shortest Distance between Point and Segment)"
date:   2019-02-22 20:00:00
categories: Algorithm
comments: true
---
* 점 p와 선분 l 사이의 최소 거리를 구하는 알고리즘

  - 선분 위에 최소 거리가 되는 점이 존재한다면 직선에서의 문제와 같지만
  - 선분의 한 끝점까지의 거리가 최소거리인 경우에는 예외처리가 필요하다.
  - ```c++
    double distToLineSegment(Point p, Point a, Point b, Point& c) {
        Vec ap = pointToVec(a, p), ab = pointToVec(a, b);
        double u = dotProduct(ap, ab) / norm_sq(ab);
        if (u < 0) { // 단위 벡터에 의한 비율에 따라 a에 가까운지 b에 가까운지 결정된다.
            c = Point(a.x, a.y);
            return dist(p, a);
        }
        if (u > 1) {
            c = Point(b.x, b.y);
            return dist(p, b);
        }
        c = translate(a, scale(ab, u));
        return dist(p, c);
    }
    ```