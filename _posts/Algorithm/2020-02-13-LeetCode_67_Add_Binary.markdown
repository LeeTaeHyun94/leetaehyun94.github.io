---
layout: post
title: "[LeetCode 67] Add Binary"
description: "[LeetCode 67] Add Binary"
date: 2020-02-13 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 67] Add Binary](https://leetcode.com/problems/add-binary/)

## 문제 요약

이진수를 나타내는 문자열 두 개가 주어졌을 때, 이진수의 덧셈 연산을 하는 함수 작성

## 풀이

올림수를 고려한 예외처리를 포함하여 구현하였다.  
풀고 나서 다른 사람들의 코드를 관찰해 본 결과, 성능에 엄청나게 큰 차이는 없지만 가독성과 효율성의 차이가 많이 났다.

## 코드

```Java
class Solution { // v1
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();
        boolean carry = false;
        int i, j;
        for (i = a.length() - 1, j = b.length() - 1; i >= 0 && j >= 0; i--, j--) {
            if (a.charAt(i) == '1') {
                if (b.charAt(j) == '1') {
                    if (carry) sb.insert(0, '1');
                    else sb.insert(0, '0');
                    carry = true;
                }
                else {
                    if (carry) {
                        sb.insert(0, '0');
                        carry = true;
                    }
                    else {
                        sb.insert(0, '1');
                        carry = false;
                    }
                }
            }
            else {
                if (b.charAt(j) == '1') {
                    if (carry) {
                        sb.insert(0, '0');
                        carry = true;
                    }
                    else {
                        sb.insert(0, '1');
                        carry = false;
                    }
                }
                else {
                    if (carry) sb.insert(0, '1');
                    else sb.insert(0, '0');
                    carry = false;
                }
            }
        }
        String s = i < 0 ? b : a;
        for (int idx = i < 0 ? j : i; idx >= 0; idx--) {
            if (s.charAt(idx) == '1') {
                if (carry) {
                    sb.insert(0, '0');
                    carry = true;
                }
                else {
                    sb.insert(0, '1');
                    carry = false;
                }
            }
            else {
                if (carry) sb.insert(0, '1');
                else sb.insert(0, '0');
                carry = false;
            }
        }
        if (carry) sb.insert(0, '1');
        return sb.toString();
    }
}

class Solution { // v2
    public String addBinary(String a, String b) {
        StringBuilder s = new StringBuilder();
        int m = a.length()-1;
        int n = b.length()-1;
        int carry =0;
        
        while(m>=0 || n>=0 || carry ==1){
            int value1 = (m>=0) ? a.charAt(m--) - '0' : 0;
            int value2 = (n>=0) ? b.charAt(n--) - '0' : 0;
            int sum = value1 + value2 + carry;
            carry = sum/2;
            s.insert(0,sum%2);
        }
        return (carry==1) ? s.insert(0,1).toString() : s.toString();
    }
}
```