---
layout: post
title:  "Graph(Topological Sort)"
description: "Graph(Topological Sort)"
date:   2019-03-06 18:54:00
categories: Algorithm
comments: true
---
일련의 정점들을 일자로 나열하는 것 (ex : 작업의 순서도, 수강 신청의 선수 과목 구조 등등)

방향이 있고 사이클이 없는 그래프(DAG : Directed Acyclic Graph)에서 가능하다.

사이클의 유무를 모르는 유향 그래프에서 위상 정렬을 수행해도 사이클의 유무를 알 수 있다. (사이클을 찾아내면 당연히 위상 정렬은 되지 않는다.)

1. 내향차수(Indegree)가 0인 정점을 찾는다.
2. 찾은 정점과 정점의 외향 간선을 제거한다.
3. 정점이 남아있다면 1 - 2 과정을 반복한다.

이것이 기존의 방법이라면 위에서 언급한 DFS를 이용한다면 DFS 한 번에 위상 정렬이 가능하다.

DFS를 진행하며 Finish Time이 늦는 순서대로 출력한다. (먼저 탐색이 끝나는 대로 쌓아 두었다가 역순으로 출력한다.) => Topological Ordering

이 방식은 DFS가 가장 빨리 끝나는 정점이 외향 차수(Outdegree)가 0이고 방향 또한 가장 깊은 곳이기 때문에 그만큼 거쳐온 정점도 많다는 DFS의 특징을 이용한 방식이다.
