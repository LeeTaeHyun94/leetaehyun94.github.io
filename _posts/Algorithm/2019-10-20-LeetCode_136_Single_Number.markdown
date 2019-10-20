---
layout: post
title: "[LeetCode 136] Single Number"
description: "[LeetCode 136] Single Number"
date: 2019-10-20 14:29:00
categories: Algorithm
comments: true
---
[[LeetCode 136] Single Number](https://leetcode.com/problems/single-number/)

## 문제 요약

하나를 제외하고 모든 정수들이 두 개씩 존재하는 비어있지 않은 배열이 주어졌을 때, 오로지 한 개만 존재하는 정수를 찾는 문제.

## 풀이

추가적인 배열이나 해시 테이블을 사용하여 각 정수가 몇 번씩 나오는지 개수를 세고 한 번만 나오는 정수를 찾는 방법이 가장 먼저 떠오른다.  
추가 메모리를 사용하지 않고 푸는 방법은 XOR 연산을 이용하는 것인데, XOR 연산의 특징은 이진수에서 비트 별로 같은 수를 만나면 0, 다른 수를 만나면 1이 된다.  
이 특징을 이용해 처음엔 0으로 시작해서 어떤 숫자를 한 번 XOR 연산을 하게 되면, 그 숫자가 남게 되고 두 번 XOR 연산을 하게 되면 그 숫자가 사라지게 된다.  
cf) XOR 연산은 temp 변수를 쓰지 않는 swap 연산에도 이용된다.

## 코드

```Java
class Solution {
    public int singleNumber(int[] nums) {
        int ret = 0;
        for (int i = 0; i < nums.length; i++) ret ^= nums[i];
        return ret;
    }
}
```
