---
layout: post
title: "[LeetCode 70] Climbing Stairs"
description: "[LeetCode 70] Climbing Stairs"
date: 2020-02-12 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 70] Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

## 문제 요약

계단을 올라가는 방법은 한 칸 올라가기, 두 칸 올라가기 두 가지 방법 밖에 없고 계단의 수가 주어졌을 때, 계단을 오르는 경우의 수를 구하는 문제.

## 풀이

계단을 올라가는 방법에는 두 가지 밖에 없기 때문에 예를 들어 세 칸을 올라가는 방법은 i) 첫 번째 칸의 계단에서 두 칸 오르는 경우, ii) 두 번째 칸의 계단에서 한 칸 오르는 경우 이렇게 두 가지로 나눌 수 있다.  
즉, n 칸의 계단을 오르는 경우의 수는 n-1 번째 칸의 계단과 n-2 번째 칸의 계단을 오르는 경우의 수와 연관이 있다는 얘기이다.  
정확히 말해 부분 문제로 나누어 생각할 수 있다는 것이다. 이를 기반으로 곰곰히 생각해보면 규칙성을 찾을 수 있다. (일종의 DP 문제)

## 코드

```Java
class Solution {
    public int climbStairs(int n) {
        if (n < 2) return 1;
        if (n < 3) return 2;
        int[] dp = new int[3];
        dp[0] = 1;
        dp[1] = 2;
        for (int i = 3; i <= n; i++) {
            dp[2] = dp[0] + dp[1];
            dp[0] = dp[1];
            dp[1] = dp[2];
        }
        return dp[1];
    }
}
```