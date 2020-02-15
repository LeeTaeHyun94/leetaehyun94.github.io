---
layout: post
title: "[LeetCode 58] Length of Last Word"
description: "[LeetCode 58] Length of Last Word"
date: 2020-02-15 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 58] Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

## 문제 요약

소문자, 대문자, 공백을 포함한 문자열이 주어졌을 때, 문제 이름 그대로 마지막 단어의 길이를 출력하는 문제.

## 풀이

간단한 구현문제지만, 연속으로 공백문자가 나온다던가 끝이 공백으로 끝나는 등 이상한(?) 케이스들이 있다...  
그래서 오히려 주어진 문자열을 뒤에서부터 확인하는 편이 구현이 간단한 것 같다.

## 코드

```Java
class Solution {
    public int lengthOfLastWord(String s) {
        int cnt = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == ' ') {
                if (cnt > 0) break;
                continue;
            }
            else cnt++;
        }
        return cnt;
    }
}
```