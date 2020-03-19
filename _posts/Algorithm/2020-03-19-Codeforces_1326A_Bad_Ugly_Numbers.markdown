---
layout: post
title: "[Codeforces 1326A] Bad Ugly Numbers"
description: "[Codeforces 1326A] Bad Ugly Numbers"
date: 2020-03-19 18:04:00
categories: Algorithm
comments: true
---
[[Codeforces 1326A] Bad Ugly Numbers](https://codeforces.com/contest/1326/problem/A)

## 문제 요약

양의 정수 n이 주어졌을 때, 각 자릿수로 나누어 떨어지지 않고, n개의 자릿수를 갖는 양의 정수를 구하는 문제

## 풀이

n의 범위가 100000까지므로 일반적인 정수를 구해 자릿수로 나누어 떨어지지 않는지 확인하는 방법으로는 한계가 있음을 알 수 있다.  
문제의 조건에 해당하는 숫자를 만드는 방법에는 여러 가지가 있겠지만, 내가 생각한 방법은 첫 번째 자리에 2를 넣고 나머지 자릿수에 3을 넣는 방법이다.  
내 아이디어는 3의 배수 중에 3으로 끝나는 것은 11, 21, 31 ... 일의 자리가 1로 끝나는 수의 배수일 경우 밖에 없다는 사실과 맨 앞자리에 2를 넣음으로써 3으로 나누어 떨어지지 않게 할 수 있다는 사실에 기반하였다. 끝자리가 3으로 끝나는 홀수는 2로 당연히 나누어 떨어지지 않는다.  
예외 처리로는 n이 1일 경우, 모든 한 자리 숫자가 자기 자신으로 나누어 떨어지므로 -1을 출력해야 한다.

## 코드

```C++
#include <iostream>
int T, N;
int main() {
    for (scanf("%d", &T); T--;) {
        scanf("%d", &N);
        if (N == 1) puts("-1");
        else {
            printf("2");
            for (int i = 0; i < N - 1; i++) printf("3");
            puts("");
        }
    }
    return 0;
}
```
