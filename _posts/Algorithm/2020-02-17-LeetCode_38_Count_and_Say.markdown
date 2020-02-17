---
layout: post
title: "[LeetCode 38] Count and Say"
description: "[LeetCode 38] Count and Say"
date: 2020-02-17 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 38] Count and Say](https://leetcode.com/problems/count-and-say/)

## 문제 요약

정수 N(1 <= N <= 30)이 주어졌을 때, 1부터 시작하여 숫자의 개수와 숫자를 이어 붙여 증가하는 수열의 형태를 출력하는 문제  
예시 - 1 (한 개의 1이 있다.) -> 11 (11은 1이 두 개 있으므로 두 개의 1이 있다.) -> 21 (2가 하나, 1이 하나) -> 1211 -> ...

## 풀이

규칙에 따라 반복문을 활용하여 구현하였다.
주의해야 할 점은 자바로 문자열 연산을 할 때 '+' 덧셈 연산을 함부로 하게 되면 시간과 메모리를 추가적으로 소모하게 된다. (내부적으로 새로운 String을 생성하는 것 같다.)

## 코드

```Java
class Solution {
    public String countAndSay(int n) {
        String s = "1";
        for (int i = 2; i <= n; i++) {
            int cnt = 1;
            char num = s.charAt(0);
            StringBuilder sb = new StringBuilder();
            for (int j = 1; j < s.length(); j++) {
                char c = s.charAt(j);
                if (num != c) {
                    sb.append(cnt).append(num);
                    num = c;
                    cnt = 1;
                }
                else cnt++;
            }
            sb.append(cnt).append(num);
            s = sb.toString();
        }
        return s;
    }
}
```