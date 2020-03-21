---
layout: post
title: "[Codeforces 1326C] Permutation Partitions"
description: "[Codeforces 1326C] Permutation Partitions"
date: 2020-03-21 18:04:00
categories: Algorithm
comments: true
---
[[Codeforces 1326C] Permutation Partitions](https://codeforces.com/contest/1326/problem/C)

## 문제 요약

양의 정수 n, k가 주어지고, n보다 작은 양의 정수가 n개 있는 배열이 주어졌을 때, 해당 배열을 k개의 구간으로 쪼개어 각 구간의 최댓값 합이 최대가 되는 값을 구하고, 해당 경우의 수를 구하는 문제

## 풀이

단순히 생각해보면 k개의 구간으로 나누는 경우의 수를 모두 고려해야 할 것 같지만, k개의 구간의 최댓값을 미리 고정시켜놓는 그리디한 방법을 떠올리면 해결 가능하다.  
그래서 주어진 배열을 정렬하여 k개의 구간의 최댓값이 될 k개의 최댓값과 인덱스를 구하고, 배열의 인덱스를 처음부터 차례대로 보면서 해당 구간의 끝 지점이 될 수 있는 경우의 수를 모두 곱하면 된다.  
주의해야 할 점은 경우의 수에만 모듈러 연산을 할 것.


## 코드

```C++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int n, k;
long long ans1, ans2 = 1;
pair<long long, long long> arr[200000];
int main() {
    scanf("%d %d", &n, &k);
    int m = 0;
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i].first);
        arr[i].second = i;
    }
    sort(arr, arr + n);
    vector<long long> idxs;
    for (int i = 0; i < k; i++) {
        ans1 += arr[n - i - 1].first;
        idxs.push_back(arr[n - i - 1].second);
    }
    printf("%lld ", ans1);
    sort(idxs.begin(), idxs.end());
    for (int i = 0; i < k - 1; i++)
        ans2 = ans2 * (idxs[i + 1] - idxs[i]) % 998244353;
    printf("%lld ", ans2);
    return 0;
}
```
