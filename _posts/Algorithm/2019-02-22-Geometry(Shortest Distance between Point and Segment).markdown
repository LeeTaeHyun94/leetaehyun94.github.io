---
layout: post
title:  "Geometry(Shortest Distance between Point and Segment)"
description: "Computational Geometry(Shortest Distance between Point and Segment)"
date:   2019-02-21 20:00:00
categories: Algorithm
comments: true
---
* 점 p와 직선 l (점 a, b에 의해 결정) 사이의 최소 거리를 구하는 알고리즘

  - 점 p와 가장 가까운 직선 l 위의 점 c를 구한다.

  - 점 p와 c 사이의 유클리드 거리를 구한다. 이 때, 점 c를 벡터 ab에 u 배율 곱한 것에 따라 평행이동시킨 점으로 생각할 수 있다.

  - u의 값을 구하기 위해서는 내적을 이용하여 벡터 ap를 ab로 스칼라 사영하면 된다.

  - ```c++
    double dotProduct(Vec a, Vec b) { return a.x * b.x + a.y * b.y; } // 벡터 크기의 내적
    double norm_sq(Vec v) { return v.x * v.x + v.y * v.y; } // 벡터 크기의 제곱
    double distToLine(Point p, Point a, Point b, Point& c) { // a, b로 벡터 구성
        Vec ap = pointToVec(a, p), ab = pointToVec(a, b); // 필요한 벡터 ap, ab 구성
        double u = dotProduct(ap, ab) / norm_sq(ab); // 단위 벡터
        // 배율을 구하기 위해 벡터 ap와 ab의 내적을 벡터 ab 제곱으로 나누어 비율을 구한다.
        c = translate(a, scale(ab, u));
        // 구한 비율에 따라 벡터를 확대, 축소한 뒤 점 a를 평행이동한 뒤
        return dist(p, c); // 점 p와 c 사이의 거리를 반환한다.
    } // 벡터 ab(로 구한 점 c)와 점 p사이의 거리
    ```