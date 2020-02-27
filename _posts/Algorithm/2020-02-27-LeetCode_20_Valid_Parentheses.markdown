---
layout: post
title: "[LeetCode 20] Valid Parentheses"
description: "[LeetCode 20] Valid Parentheses"
date: 2020-02-27 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 20] Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

## 문제 요약

괄호 문자('(', ')', '{', '}', '[', ']')로만 이루어진 문자열이 주어졌을 때 해당 괄호 문자열은 유효한 문자열인지 확인하는 아주 유명한 문제.  

## 풀이

열린 괄호를 만나면 스택에 저장하고 닫힌 괄호를 만나면 스택에 저장되어 있는, 즉 가장 최근에 열렸던 괄호와 짝이 맞는지를 검사하여 괄호 문자열의 유효성을 판별해준다.
괄호 문자열의 길이가 N이라면, O(N)의 시간복잡도를 갖는다.  

## 코드

```Java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(' || c == '{' || c == '[') st.push(c);
            else if (c == ')') {
                if (st.empty() || st.peek() != '(') return false;
                else st.pop();
            }
            else if (c == '}') {
                if (st.empty() || st.peek() != '{') return false;
                else st.pop();
            }
            else if (c == ']') {
                if (st.empty() || st.peek() != '[') return false;
                else st.pop();
            }
            else return false;
        }
        return st.empty() ? true : false;
    }
}
```