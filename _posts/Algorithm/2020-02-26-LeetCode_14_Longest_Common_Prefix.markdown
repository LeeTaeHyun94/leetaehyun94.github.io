---
layout: post
title: "[LeetCode 14] Longest Common Prefix"
description: "[LeetCode 14] Longest Common Prefix"
date: 2020-02-26 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 14] Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

## 문제 요약

문자열 배열이 주어졌을 때, 모든 문자열들의 공통된 가장 긴 접두사를 구하는 문제

## 풀이

모든 문자열들의 공통된 가장 긴 접두사라는 것은 말이 복잡해보이지 실은 간단하다.  
각 문자열의 첫 번째 인덱스부터 끝까지 스펠링 하나씩 검사하여 모든 문자열들이 처음부터 가지고 있는 스펠링이 모두 같다면 이를 공통 접두사라고 할 수 있다.  
문자열들의 개수가 N, 문자열 중에 가장 짧은 길이가 M이라고 한다면, O(NM)의 시간복잡도를 갖는다.

## 코드

```Java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        StringBuilder ret = new StringBuilder();
        if (strs.length > 0)
            for (int i = 0; 0 < strs[0].length() && i < strs[0].length(); i++) {
                char st = strs[0].charAt(i);
                boolean isAllSame = true;
                for (int j = 1; j < strs.length; j++) {
                    if (strs[j].length() <= i || strs[j].charAt(i) != st) {
                        isAllSame = false;
                        break;
                    }
                }
                if (isAllSame) ret.append(st);
                else break;
            }
        return ret.toString();
    }
}
```