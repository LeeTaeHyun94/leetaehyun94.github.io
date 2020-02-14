---
layout: post
title: "[LeetCode 66] Plus One"
description: "[LeetCode 66] Plus One"
date: 2020-02-14 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 66] Plus One](https://leetcode.com/problems/plus-one/)

## 문제 요약

양의 정수가 자릿수 별로 끊어 배열로 주어졌을 때, 이 양의 정수에 1을 더한 결과(마지막 자리에 1을 더한다.)를 똑같이 배열로 반환하는 문제.

## 풀이

올림수를 고려한 예외처리를 포함하여 구현하였다.

## 코드

```Java
class Solution {
    public int[] plusOne(int[] digits) {
        boolean carry = true;
        for (int i = digits.length - 1; carry && i >= 0; i--) {
            carry = false;
            digits[i]++;
            if (digits[i] == 10) {
                digits[i] = 0;
                carry = true;
            }
        }
        if (carry) {
            int[] ret = new int[digits.length + 1];
            ret[0] = 1;
            for (int i = 1; i < ret.length; i++) ret[i] = digits[i - 1];
            return ret;
        }
        return digits;
    }
}
```