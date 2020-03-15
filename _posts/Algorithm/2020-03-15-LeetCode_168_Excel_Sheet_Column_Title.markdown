---
layout: post
title: "[LeetCode 168] Excel Sheet Column Title"
description: "[LeetCode 168] Excel Sheet Column Title"
date: 2020-03-15 14:01:00
categories: Algorithm
comments: true
---
[[LeetCode 168] Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

## 문제 요약

양의 정수 하나가 주어졌을 때, 해당 양의 정수를 엑셀 시트의 컬럼 번호로 변환하는 문제

## 풀이

엑셀 시트의 컬럼 번호는 A~Z까지 알파벳으로 표기되므로 26진수로 변환하는 문제이다.

## 코드

```Java
class Solution {
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n > 0) {
            sb.append(n % 26 == 0 ? 'Z' : (char)('A' + n % 26 - 1));
            if (n % 26 == 0) {
                n /= 26;
                n--;
            }
            else n /= 26;
        }
        sb.reverse();
        return sb.toString();
    }
}
```
