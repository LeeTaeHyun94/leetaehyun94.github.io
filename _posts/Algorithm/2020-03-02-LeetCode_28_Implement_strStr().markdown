---
layout: post
title:  "[LeetCode 28] Implement strStr()"
description:  "[LeetCode 28] Implement strStr()"
date:   2020-03-02 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 28] Implement strStr()](https://leetcode.com/problems/implement-strstr/)

## 문제 요약

주어진 문자열(건초더미)에서 특정 문자열(바늘 문자열)의 존재 여부를 판별하는 문제

## 풀이

2중 반복문을 통해 완전탐색하는 알고리즘
KMP 알고리즘을 활용하면 더욱 빠르다.(문제를 풀게 된지 얼마 되지 않아 보지 않고 KMP 알고리즘을 작성할 수 없어서 충분한 연습을 통해 문제 풀이에 익숙해진 뒤 작성해야 겠다.)

## 코드

```Java
class Solution {
    public int strStr(String haystack, String needle) {
        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            boolean isFound = true;
            for (int j = 0; j < needle.length(); j++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    isFound = false;
                    break;
                }
            }
            if (isFound) return i;
        }
        return -1;
    }
}
```