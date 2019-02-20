---
layout: post
title:  "Geometry(Vector)"
description: "Computational Geometry(Vector)"
date:   2019-02-20 21:55:00
categories: Algorithm
comments: true
---
```c++
struct Vec {
    double x, y;
    
    vec(double _x, double _y) : x(_x), y(_y) {}
}; // x와 y의 증감량을 통해 표현

Vec pointToVec(Point a, Point b) {
    return vec(b.x - a.x, b.y - a.y);
} // 두 점을 a -> b 방향의 벡터로 변환

Vec scale(Vec v, double s) {
    return Vec(v.x * s, v.y * s);
} // 벡터의 확대, 축소

Point translate(Point p, Vec v) {
    return Point(p.x + v.x, p.y + v.y);
} // 점을 벡터에 따라 평행이동
```

cf) 자연계에는 스칼라(Scalar)와 벡터(Vector) 두 종류의 물리량이 있다.

- Scalar : 크기(Magnitude)만을 갖는 물리량 (움직임으로 따지면 속력(단위 시간 당 이동한 거리))
- Vector : 크기와 방향을 동시에 갖는 물리량 (움직임으로 따지면 속도(단위 시간 당 이동한 변위))
  - 시작점에서 끝 점에 이르는 길이(크기)와 방향을 나타내는 벡터량, 힘
  - 노름(norm) : 벡터의 크기를 나타내는 절대값, 스칼라와 똑같이 표현되어 구별하기 위해 노름이라고 한다.
- 벡터의 곱
  - 내적 (Dot Product, Inner Product, 스칼라 곱 : Scalar Product) : 연산 결과가 스칼라로 나온다.
    - 평면 벡터의 내적
      - ![평면 벡터의 내적 공식](../../assets/Algorithm/1.PNG)
    - 공간 벡터의 내적
      - ![공간 벡터의 내적 공식](../../assets/Algorithm/2.PNG)
      - 이는 코사인 제 2 법칙으로 증명 가능하다.
        - ![삼각형](../../assets/Algorithm/3.PNG)
  - 외적 (Cross Product, Outer Product, Vector Product) : 오른손(나사)의 법칙을 기준으로 정의하겠다.
    - A X B = AB sin a (a = 벡터 A와 B의 사잇각) : 벡터 B가 벡터 A를 기준으로 얼마나 회전하려는 성질을 가지는가. 벡터 A와 벡터 B의 수직 벡터가 결과값
    - ![외적](../../assets/Algorithm/4.PNG)
    - ![외적 공식](../../assets/Algorithm/5.PNG) <= 비호환(non-commutative) 연산
    - 단위 벡터(Unit Vector) i, j, k 사이의 외적을 생각해보자. (단위 벡터들의 크기는 모두 1)
      - 자기 자신과의 외적은 사잇각이 0도이므로(sin0 = 0) 당연히 0이다.
      - 단위 벡터 i, j의 외적은 사잇각이 90도이므로(sin90 = 1) 1이다.
        - ![sin](../../assets/Algorithm/6.PNG) ![오른손 법칙](../../assets/Algorithm/7.PNG)
      - 오른손 법칙을 기준으로 했기 때문에 i X j = k, j X i = -k
      - ![두 벡터의 외적 공식](../../assets/Algorithm/8.PNG)
      - 이는 행렬식으로도 표현 가능하다.
        - ![두 벡터의 외적 행렬식](../../assets/Algorithm/9.PNG)
        - 때문에 두 벡터의 외적을 구한다는 것은 행렬식의 사루스 전개 혹은 소행렬식을 구하는 것과 같다.
        - ![사선 정리](../../assets/Algorithm/10.PNG)
        - ![사루스](../../assets/Algorithm/11.PNG)
    - 벡터의 외적은 두 벡터로 구성된 평행사변형의 넓이라고도 할 수 있다.
      - 때문에 두 벡터를 구성할 수 있는 세 점을 통해 삼각형의 넓이 또한 구할 수 있다.
        - (외적) / 2
    - 두 벡터의 외적은 두 벡터의 사잇각이 180도보다 클 때는 음수가 된다.
      - 180도 일때는 일직선 상에 놓여있다, 180도보다 작을 때는 양수가 된다.