---
layout: post
title: "[LeetCode 13] Roman to Integer"
description: "[LeetCode 13] Roman to Integer"
date: 2020-02-25 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 13] Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

## 문제 요약

로마 숫자를 표현하는 문자열이 주어졌을 때, 해당 로마 숫자 문자열을 정수로 변환하는 문제.

## 풀이

문제의 설명대로 특정 로마 숫자 앞에 올 수 있는 다른 로마 숫자는 정해져 있다. 이에 대한 예외처리만 제대로 실수없이 추가한다면 그리 어렵지 않은 구현 문제이다.  
로마 숫자 문자열의 개수가 N이라고 한다면, O(N)의 시간복잡도를 갖는다.

## 코드

```Java
class Solution {
    public int romanToInt(String s) {
        int ret = 0;
        for (int i = 0; i < s.length();) {
            if (s.charAt(i) == 'I') {
                if (i + 1 < s.length()) {
                    if (s.charAt(i + 1) == 'V') {
                        ret += 4;
                        i += 2;
                    }
                    else if (s.charAt(i + 1) == 'X') {
                        ret += 9;
                        i += 2;
                    }
                    else {
                        ret++;
                        i++;
                    }
                }
                else {
                    ret++;
                    i++;
                }
            }
            else if (s.charAt(i) == 'V') {
                ret += 5;
                i++;
            }
            else if (s.charAt(i) == 'X') {
                if (i + 1 < s.length()) {
                    if (s.charAt(i + 1) == 'L') {
                        ret += 40;
                        i += 2;
                    }
                    else if (s.charAt(i + 1) == 'C') {
                        ret += 90;
                        i += 2;
                    }
                    else {
                        ret += 10;
                        i++;
                    }
                }
                else {
                    ret += 10;
                    i++;
                }
            }
            else if (s.charAt(i) == 'L') {
                ret += 50;
                i++;
            }
            else if (s.charAt(i) == 'C') {
                if (i + 1 < s.length()) {
                    if (s.charAt(i + 1) == 'D') {
                        ret += 400;
                        i += 2;
                    }
                    else if (s.charAt(i + 1) == 'M') {
                        ret += 900;
                        i += 2;
                    }
                    else {
                        ret += 100;
                        i++;
                    }
                }
                else {
                    ret += 100;
                    i++;
                }
            }
            else if (s.charAt(i) == 'D') {
                ret += 500;
                i++;
            }
            else if (s.charAt(i) == 'M') {
                ret += 1000;
                i++;
            }
        }
        return ret;
    }
}
```