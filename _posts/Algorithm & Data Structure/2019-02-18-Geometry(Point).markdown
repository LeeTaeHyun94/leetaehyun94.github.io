---
layout: post
title:  "Geometry(Point)"
description: "Computational Geometry(Point)"
date:   2019-02-18 21:50:00
categories: Algorithm
comments: true
---
```c++
struct Point_i {
	int x, y;
	Point_i() { x = y = 0; }
	Point_i(int _x, int _y) : x(_x), y(_y) {}
}; // 좌표가 정수 값으로 주어질 때

struct Point {
	double x, y;

	Point() { x = y = 0.0; }

	Point(double _x, double _y) : x(_x), y(_y) {}

	bool operator < (Point p) const { // 연산자 재정의, EPS : 1e^-9와 같은 아주 작은 값 (문제에 따라 오차 범위 지정)
		if (fabs(x - p.x) > EPS) return x < p.x; // fabs() : double 자료형의 절대값
		return y < p.y;
	}

	bool operator == (Point p) const {
		return fabs(x - p.x) < EPS && fabs(y - p.y) < EPS;
	} // 두 점이 서로 같은지 비교
}; // 좌표가 실수 값으로 주어질 때

double hypot(double x, double y) { return sqrt(x * x + y * y); }
// 피타고라스의 정리에 의하여 z = root(x^2 + y^2)
double dist(Point p1, Point p2) { return hypot(p1.x - p2.x, p1.y - p2.y); }
// Get Euclidean Distance

Point rotate(Point p, double theta) {
	double rad = theta * (PI / 180.0); // degree를 radian으로 변환!
	// deg = rad * (180.0 / PI)
	return Point(p.x * cos(rad) - p.y * sin(rad), p.x * sin(rad) + p.y * cos(rad));
} // p를 원점(0, 0)을 중심으로 반시계 방향으로 theta도 회전한다.
```

* 극좌표계 : 평면 위의 위치를 각도와 거리를 써서 나타내는 2차원 좌표계, 두 점 사이의 관계가 각이나 거리로 쉽게 표현되는 경우에 가장 유용하다. 
  직교 좌표계에서는 삼각함수로 복잡하게 나타나는 관계가 극좌표계에서는 간단하게 표현되는 경우가 많다. 
  2차원 좌표계이기 때문에 극좌표는 반지름 성분과  각 성분의 두 성분으로 결정되며 주로 r로 나타내는 반지름 성분은 극(원점)에서의 거리를 나타낸다.
  주로 Θ로 나타내는 각 성분은 0°(직교 좌표계에서 x축의 양의 방향에 해당)에서 반시계 방향으로 잰 각의 크기를 나타낸다.
* rotate에 대한 일반화 : 각도라는 개념이 없는 직교좌표계에서는 점 P(x, y)를 각 α만큼 회전시킨다고 하면 표현하기 어렵다.  
     하지만 극좌표계에서는 P(r, Θ) -> P'(r, Θ+α) 이처럼 쉽게 표현이 가능하다. 이렇게 표현한 극좌표를    
     ?		 삼각함수를 이용해 데카르트 좌표로 변환하면 P'(x', y') = P`(r * cos(Θ+α), r * sin(Θ+α))가 되고  
     ?		 삼각함수의 덧셈정리를 이용해 P'(r*cosΘcosα - r*sinΘsinα, r*sinΘcosα + r*cosΘsinα)가 된다.  
     ?		 위 식에서 r*cosΘ = P.x, r*sinΘ = P.y이므로 위의 rotate 함수처럼 일반화가 가능하다.