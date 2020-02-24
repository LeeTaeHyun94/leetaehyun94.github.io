---
layout: post
title: "[LeetCode 9] Palindrome Number"
description: "[LeetCode 9] Palindrome Number"
date: 2020-02-24 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 9] Palindrome Number](https://leetcode.com/problems/palindrome-number/)

## 문제 요약

하나의 정수가 주어졌을 때, 해당 정수가 회문인 숫자인지 판별하는 문제.

## 풀이

나는 정수를 한 자리씩 분리하여 ArrayList에 저장한 뒤, 하나씩 비교하는 코드를 작성하였다.  
조금 더 효율적인 방안을 생각해보니 하나의 정수를 자릿수가 같거나 하나 차이나는 두 개의 정수로 분리하여 자릿수가 같을 경우엔 두 수가 같은지, 하나 차이날 경우엔 자릿수가 큰 쪽에 10을 나눠 같은지를 판별하면 시간과 공간 복잡도를 아낄 수 있다.  
정수를 분리하는 방법은 10으로 나머지 연산과 나눗셈 연산을 반복하면 분리할 수 있다.  
두 개의 정수(원래 정수는 A, 분리한 나머지 절반은 B로 가정)로 분리할 때는 A > B가 될 때까지 분리하면 된다. (이 경우 위와 마찬가지로 주어진 정수의 자릿수가 N개라면 시간복잡도는 O(N)이긴 하지만 엄밀히 따져보면 O(N/2)이다.)

## 코드

```Java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) return false;
        List<Integer> arr = new ArrayList<>();
        while (x > 0) {
            arr.add(x % 10);
            x /= 10;            
        }
        for (int i = 0, j = arr.size() - i - 1; i < j; i++, j--)
            if (arr.get(i) != arr.get(j)) return false;
        return true;
    }
}
```