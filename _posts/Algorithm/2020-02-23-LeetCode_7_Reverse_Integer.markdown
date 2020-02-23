---
layout: post
title: "[LeetCode 7] Reverse Integer"
description: "[LeetCode 7] Reverse Integer"
date: 2020-02-23 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 7] Reverse Integer](https://leetcode.com/problems/reverse-integer/)

## 문제 요약

하나의 정수가 주어졌을 때, 해당 정수를 거꾸로 뒤집는 문제.

## 풀이

정수를 분리하는 방법은 10으로 나머지 연산과 나눗셈 연산을 반복하면 분리할 수 있다.  
기존의 정수에서는 한 자리씩 분리하고 뒤집을 정수에 10을 곱해주면서 자릿수를 미는 방식을 활용.  
주의해야 할 점은 엣지 케이스로 주어지는 정수가 한계치에 가까운 21억의 숫자(음수 포함)가 있는데 끝자리가 2 이상만 돼도 오버플로우가 발생할 수 있다. (사실 문제에 적혀있는데 제대로 읽지 않아 발생한 참사..)  
때문에, 뒤집을 정수를 저장할 변수의 자료형을 long으로 지정하고 뒤집고 나서 Integer.MIN_VALUE보다 작거나 Integer.MAX_VALUE보다 큰 경우를 확인하여 0을 반환해야 한다.  
주어진 정수의 자릿수가 N개라면 시간복잡도는 O(N)이다.

## 코드

```Java
class Solution {
    public int reverse(int x) {
        long ret = 0;
        while (x != 0) {
            ret *= 10;
            ret += x % 10;
            x /= 10;
        }
        return (ret < Integer.MIN_VALUE || ret > Integer.MAX_VALUE) ? 0 : (int)ret;
    }
}
```