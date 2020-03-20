---
layout: post
title: "[Codeforces 1326B] Maximums"
description: "[Codeforces 1326B] Maximums"
date: 2020-03-20 18:04:00
categories: Algorithm
comments: true
---
[[Codeforces 1326B] Maximums](https://codeforces.com/contest/1326/problem/B)

## 문제 요약

문제 요약이 간결히 되지 않아 사진 첨부로 대체합니다.  
![[Codeforces 1326B] Maximums-1](./../../assets/Algorithm/20.PNG)
![[Codeforces 1326B] Maximums-2](./../../assets/Algorithm/21.PNG)

## 풀이

처음에 문제가 복잡하게 서술되어 있어 이해가 쉽지 않지만, 간략히 요약하자면 어떤 규칙에 의해 a 배열에서 b 배열로 변형이 일어났고, 이러한 b 배열이 주어졌을 때 역으로 a 배열을 구하는 문제이다.  
변형이 일어나는 과정은 0을 포함한 i-1번째 원소 중 최댓값만큼 a 배열의 i번째 원소에 빼주는 과정을 배열 전체에 진행한다.  
이를 역산하는 과정을 구현하면 되는데 간단하다.  
0을 포함한 i-1번째 원소 중 최댓값을 m이라고 가정하면, m은 처음에 0에서 시작해서 m = max(m, bi + m)의 조건으로 갱신할 수 있다.  
주의해야 할 점은 ai 값을 먼저 구한 다음 m을 갱신해야 한다.


## 코드

```C++
#include <iostream>
#include <algorithm>
using namespace std;
int n;
int main() {
    scanf("%d", &n);
    int m = 0;
    for (int i = 0, num; i < n; i++) {
        scanf("%d", &num);
        printf("%d ", num + m);
        m = max(m, num + m);
    }
    return 0;
}
```
