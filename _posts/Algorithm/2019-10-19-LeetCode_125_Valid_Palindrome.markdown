---
layout: post
title: "[LeetCode 125] Valid Palindrome"
description: "[LeetCode 125] Valid Palindrome"
date: 2019-10-19 17:06:00
categories: Algorithm
comments: true
---
[[LeetCode 125] Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

## 문제 요약

문자열이 주어졌을 때, 해당 문자열의 알파벳 대소문자와 숫자만 포함하여 회문인지를 판별하는 문제.

## 풀이

알파벳 대소문자와 숫자만을 남기는 전처리를 통해 새로운 문자열을 만든 뒤 회문임을 판별한다.

## 코드

```Java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (('a' <= c && c <= 'z') || ('0' <= c && c <= '9')) sb.append(c);
            else if ('A' <= c && c <= 'Z') sb.append((char)(c - 'A' + 'a'));
        }
        String ss = sb.toString();
        for (int i = 0; i < ss.length() / 2; i++)
            if (ss.charAt(i) != ss.charAt(ss.length() - 1 - i)) return false;
        return true;
    }
}
```
