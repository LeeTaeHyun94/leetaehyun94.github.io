---
layout: post
title: "[Codeforces 1323B] Count Subrectangles"
description: "[Codeforces 1323B] Count Subrectangles"
date: 2020-03-09 14:15:00
categories: Algorithm
comments: true
---
[[Codeforces 1323B] Count Subrectangles](https://codeforces.com/contest/1323/problem/B)

## 문제 요약

행의 개수를 나타내는 양의 정수 n, 열의 개수를 나타내는 양의 정수 m이 주어지고, 0과 1로 구성된 n x m 크기의 행렬을 나타내는 배열 두 개가 주어졌을 때,  
크기가 k인 부분 사각형의 개수를 구하는 문제.

## 풀이

n과 m의 범위가 최대 40000이므로 완전탐색으로는 해결 불가능하다는 것을 알 수 있다.  
연속된 1로 이루어져 있어 사각형을 구성할 수 있는 구간을 전처리를 통해 미리 구하는 최적화가 필요하다.  
반복문을 통해 행과 열을 순차적으로 탐색하면서 연속된 1로 이루어진 구간을 찾고 그 구간에서 길이 1부터 n 또는 m까지 몇 개의 사각형을 만들 수 있을지 배열에 저장한다.  
그렇게 행과 열에서 길이 별로 사각형을 구성 가능한 경우의 수를 구한 다음, 한 쪽(행 또는 열)을 기준으로 길이 1부터 크기가 k인 사각형을 구성할 수 있는지 확인해주면 된다.  
사각형을 구성하는 방법은 가로 또는 세로변이 한 쪽(행은 가로에 해당, 열은 세로에 해당)을 기준으로 반복문을 통해 고정시키면서 확인하기 때문에 k를 한 쪽 변으로 나누어 떨어지는지 확인하고 나누어 떨어지는 다른 한 쪽 변의 길이를 통해 각 경우의 수를 곱해주면 해당 구간의 사각형을 구성하는 경우의 수가 된다.

## 코드

```C++
#include <iostream>
#include <vector>
using namespace std;
int n, m, k;
long long ans;
vector<int> go(vector<int> v) {
    vector<int> ret(v.size() + 1);
    int i = 0;
    while (i < v.size()) {
        if (!v[i]) {
            i++;
            continue;
        }
        int j = i;
        while (j < v.size() && v[j]) j++;
        for (int a = 1; a <= j - i; a++)
            ret[a] += j - i - a + 1;
        i = j;
    }
    return ret;
}
int main() {
    scanf("%d %d %d", &n, &m, &k);
    vector<int> N(n), M(m);
    for (int i = 0; i < n; i++) scanf("%d", &N[i]);
    for (int i = 0; i < m; i++) scanf("%d", &M[i]);
    auto res_n = go(N), res_m = go(M);
    for (int i = 1; i < res_n.size(); i++)
        if (!(k % i) && k / i <= m) ans += (long long)res_n[i] * res_m[k / i];
    printf("%lld", ans);
    return 0;
}
```
