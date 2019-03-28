---
layout: post
title:  "Geometry(CCW)"
description: "Computational Geometry(Counter Clock Wise)"
date:   2019-02-24 17:15:00
categories: Algorithm
comments: true
---
* 두 점 p와 q에 의해 결정되는 직선이 주어졌을 때, 어떤 점 r이 그 직선에 대해 어느 위치에 있는지를 구할 수 있다.

  * 점 r은 직선 pq를 기준으로 왼쪽에 있을 수도, 오른쪽에 있을 수도, 직선 상에 위치할 수도 있다.

  * 이를 벡터의 외적을 이용하면 점의 위치를 판별할 수 있다는 것이 CCW 알고리즘

  * 반시계방향 검사(알고리즘) (CCW : Counter Clock Wise, Clock Wise Algorithm) / 좌회전 검사

  * 세 점으로 부터 두 벡터 pq와 pr을 얻었다고 할 때, 두 벡터의 외적 pq X pr은 또 다른 벡터를 나타내는데, 그 벡터는 벡터 pq와 pr에 직교한다. 이 벡터의 크기는 위에서도 언급했듯이 두 벡터로 구성되는 평행사변형의 면적과 동일하다.

  * 외적의 결과가 음수인지, 0인지, 양수인지에 의해 좌, 우측, 일직선인 경우를 판별한다.

  * 정확히는 sinΘ에 의해 양수인 영역(0 < Θ < 180), 음수인 영역(180 < Θ < 360), 0인 경우(0, 180)를 판별하는 것이다.

  * ![CCW](../../assets/Algorithm/13.PNG)

  * ```c++
    double crossProduct(Vec a, Vec b) {
        return a.x * b.y - a.y + b.x;
    }
    
    int ccw(Point p, Point q, Point r) {
        double cp = crossProduct(pointToVec(p, q), pointToVec(p, r));
        if (cp < EPS) return -1;
        if (cp > EPS) return 1;
        return 0;
    }
    // 선분의 끝점이 교차점에 제외되는 경우
    bool intersectProp(Point a, Point b, Point c, Point d) {
    	return ccw(a, b, c)*ccw(a, b, d) < 0 && ccw(c, d, a)*ccw(c, d, b) < 0;
    }
    
    // 선분의 끝점이 교차점에 포함되는 경우
    bool intersect(Point a, Point b, Point c, Point d) {
    	return ccw(a, b, c)*ccw(a, b, d) <= 0 && ccw(c, d, a)*ccw(c, d, b) <= 0;
    }
    ```