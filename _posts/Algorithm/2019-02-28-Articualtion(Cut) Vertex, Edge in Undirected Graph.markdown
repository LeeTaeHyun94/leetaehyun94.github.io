---
layout: post
title:  "Articualtion(Cut) Vertex, Edge in Undirected Graph"
description: "Articualtion(Cut) Vertex, Edge in Undirected Graph"
date:   2019-02-27 15:45:00
categories: Algorithm
comments: true
---
해당 정점 혹은 간선을 연결했을 때, 연결 요소가 두 개에서 하나가 되는 정점 혹은 간선. O(V * (V + E)) => O(V + E)  

반대로 없앴을 때(단절), 하나의 연결 요소가 두 개로 되는 정점 혹은 간선.

Spanning Tree의 부모는 방문하지 않는다. 방향은 자식 노드 쪽으로. 루트는 자식 노드가 2개 이상이면 Cut Vertex가 될 수 있다.

```
* Back Edge : Spanning Tree에서 조상 노드로 올라가는 간선

* Cross Edge : Spanning Tree에서 형제 노드로 가로지르는 간선

* Forword Edge : Spanning Tree에서 자식 노드로 내려가는 간선 
```

- 단절점이 없는 그래프를 Biconnected Graph(Sub Graph, Component)라고 한다.
- 단절선은 정점이 단 두 개뿐인 이중 연결 요소라고 할 수 있다.
- 단절점/선을 일반화한 것이 연결로(Connectivity) / 간선 연결로(Edge Connectivity)