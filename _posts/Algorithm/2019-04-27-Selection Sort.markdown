---
layout: post
title:  "Selection Sort"
description: "Selection Sort"
date:   2019-04-27 18:45:00
categories: Algorithm
comments: true
---
선택 정렬은 리스트의 길이만큼 수행되는 알고리즘에 의해 원소 하나씩 정렬 상태를 만드는 정렬 방식이다.

- 선택 정렬의 특징
  - 어떤 경우에도 항상 O(N^2)의 시간복잡도를 갖는다.
  - 별도의 공간복잡도를 필요로 하지 않는 제자리 정렬 알고리즘 (in-placing sort)

1. 현재 리스트에서 조건에 맞는(가장 작거나 가장 큰) 원소를 찾는다.
2. 선택된 원소를 맨 앞에 차례대로 배치

위의 과정들을 리스트의 길이를 하나씩 줄여가며 반복하면 정렬이 완성된다.

```c++
```
