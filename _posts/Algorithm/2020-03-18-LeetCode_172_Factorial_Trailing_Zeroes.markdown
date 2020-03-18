---
layout: post
title: "[LeetCode 172] Factorial Trailing Zeroes"
description: "[LeetCode 172] Factorial Trailing Zeroes"
date: 2020-03-18 14:23:00
categories: Algorithm
comments: true
---
[[LeetCode 172] Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes/)

## 문제 요약

정수 n이 주어졌을 때, n!의 결과값에서 0이 몇개가 존재하는지 구하는 문제

## 풀이

n!의 결과값에서 0의 개수는 10이 몇 번 곱해지는지 구하면 알 수 있다.  
수학적 사실을 이용하면 n!을 하고 10으로 나눠가며 확인할 이유가 없다.  
2 * 5 = 10이기 때문에 2와 5가 몇 번 곱해지는지 구하면 되는데, 잘 생각해보면 5가 몇 번 곱해지는지 알아내면 된다.  
2의 배수보다 5의 배수가 더 적다는 사실에 기반해, 주어진 n이라는 정수에서 5로 나눠가며 5의 배수의 개수를 구하고 그 5의 배수는 수가 더 많은 어떤 2의 배수와 짝을 지어도 10의 배수를 구성할 수 있기 때문에 5의 배수의 개수만 구해주면 된다는 결론에 이른다.  
쉬운 문제처럼 보이지만, 수학적 지식이 갖춰져 있다면, 시간복잡도(O(n) -> O(logn))를 크게 줄일 수 있는 문제이다.

## 코드

```Java
class Solution {
    public int trailingZeroes(int n) {
        int ret = 0;
        while (n > 0) ret += n /= 5;
        return ret;
    }
}
```
