---
layout: post
title:  "Geometry(Line)"
description: "Computational Geometry(Line)"
date:   2019-02-19 21:55:00
categories: Algorithm
comments: true
---
```c++
struct Line {
	double a, b, c;

	Line(double _a, double _b, double _c) : a(_a), b(_b), c(_c) {}
}; // 선형 방정식의 x, y의 계수와 상수로 직선을 표현
// ax + by + c = 0

Line pointsToLine(Point p1, Point p2) {
	if (fabs(p1.x - p2.x) < EPS) return Line(1.0, 0.0, -p1.x);
	else {
		Line l;
		l.a = -(double)(p1.y - p2.y) / (p1.x - p2.x);
		l.b = 1.0; // b (y의 계수)를 1로 두어 나머지 값을 구한다. y = ax + b의 형태
		l.c = -(double)(l.a * p1.x) - p1.y;
		return l;
	}
}; // 기울기와 선형 방정식에 점의 대입을 통해 선형 방정식을 도출한다.

bool areParallel(Line l1, Line l2) {
	return fabs(l1.a - l2.a) < EPS && fabs(l1.b - l2.b) < EPS
} // 계수 a와 b를 비교하여 기울기가 같은지를 확인 (평행임을 확인)

bool areSame(Line l1, Line l2) {
	return areParallel(l1, l2) && fabs(l1.c - l2.c) < EPS
} // 평행하면서 상수항까지 같다면 일치

bool areIntersect(Line l1, Line l2, Point &p) { // 참조를 사용한 전달
	if (areParallel(l1, l2)) return false;
	p.x = (l2.b * l1.c - l1.b * l2.c) / (l2.a * l1.b - l1.a * l2.b);
	if (fabs(l1.b) > EPS) p.y = -(l1.a * p.x + l1.c);
	else p.y = -(l2.a * p.x + l2.c);
	return true;
} // 교차점이 있는지 여부와 교차점의 좌표를 구하는 함수
```

* Intersect (교차) : 만약 두 직선이 평행하지 않다면(당연히 일치할 수도 없다.) 어느 한 점에서 교차한다. 따라서 그 교점을 구하려면  
    ?    미지수가 두 개인 선형 방정식 두 개로 이루어진 연립 방정식을 풀면 된다.
* 선분은 양 끝점이 존재하며, 길이가 유한한 직선을 말한다.
* 벡터(Vector)는 선분에 방향이 더해진 것. 벡터의 x, y 성분의 크기를 멤버 변수로 하는 구조체로 표현한다.