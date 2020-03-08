---
layout: post
title: "[Codeforces 1323A] Even Subset Sum Problem"
description: "[Codeforces 1323A] Even Subset Sum Problem"
date: 2020-03-08 15:50:00
categories: Algorithm
comments: true
---
[[Codeforces 1323A] Even Subset Sum Problem](https://codeforces.com/contest/1323/problem/A)

## 문제 요약

테스트 케이스의 개수가 주어지고 각 테스트 케이스에서 N개의 정수가 주어졌을 때, 1개 이상의 정수를 합하여 짝수가 되는 경우 중 한 가지를 구하는 문제

## 풀이

간단한 문제임을 알 수 있다.  
한 개 이상의 정수를 합하여 짝수가 되는 경우는 한 개 이상의 짝수들의 합 or 짝수 개의 홀수들의 합, 이 두 가지 경우인데,  
경우의 수나 모든 경우를 구하는 것이 아니기 때문에 한 개의 짝수나 두 개의 홀수를 발견했을 때의 경우를 출력하면 된다.

## 코드

```C++
#include <iostream>
using namespace std;
int t, n;
int main() {
    for (scanf("%d", &t); t--;) {
        scanf("%d", &n);
        int even_or_odd = -1, ans[] = {0,0};
        for (int i = 1, num; i <= n; i++) {
            scanf("%d", &num);
            if (even_or_odd < 0) {
                if (num & 1) {
                    if (ans[0]) {
                        ans[1] = i;
                        even_or_odd = 1;
                    } else ans[0] = i;
                } else {
                    ans[0] = i;
                    even_or_odd = 0;
                }
            }
        }
        if (even_or_odd == -1) puts("-1");
        else if (even_or_odd) printf("2\n%d %d\n", ans[0], ans[1]);
        else printf("1\n%d\n", ans[0]);
    }
    return 0;
}
```
