---
layout: post
title:  "Geometry(Get Angle aob)"
description: "Computational Geometry(Get Angle aob)"
date:   2019-02-23 17:05:00
categories: Algorithm
comments: true
---
* 세 점 a, o, b가 주어졌을 때, 내적을 이용하여 각 aob의 크기를 구할 수 있다.

  * ![Get Angle aob](../../assets/Algorithm/12.PNG)

  * ```c++
    double angle(Point a, Point o, Point b) {
        Vec oa = pointToVec(o, a), ob = pointToVec(o, b);
        return acos(dotProduct(oa, ob) / sqrt(norm_sq(oa) * norm_sq(ob)));
    }
    ```