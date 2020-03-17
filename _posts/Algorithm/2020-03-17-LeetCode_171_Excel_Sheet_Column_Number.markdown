---
layout: post
title: "[LeetCode 171] Excel Sheet Column Number"
description: "[LeetCode 171] Excel Sheet Column Number"
date: 2020-03-17 14:56:00
categories: Algorithm
comments: true
---
[[LeetCode 171] Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number/)

## 문제 요약

엑셀 시트의 컬럼 번호를 의미하는 알파벳 대문자로 이루어진 문자열 하나가 주어졌을 때, 해당 문자열을 10진수로 변환하는 문제

## 풀이

엑셀 시트의 컬럼 번호는 A~Z까지 알파벳으로 표기되므로 26진수를 10진수로 변환하는 문제이다.

## 코드

```Java
class Solution {
    public int titleToNumber(String s) {
        int num = 1, ret = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            ret += num * (s.charAt(i) - 'A' + 1);
            num *= 26;
        }
        return ret;
    }
}
```
