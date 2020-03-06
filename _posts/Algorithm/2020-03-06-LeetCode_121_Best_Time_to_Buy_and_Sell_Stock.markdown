---
layout: post
title: "[LeetCode 121] Best Time to Buy and Sell Stock"
description: "[LeetCode 121] Best Time to Buy and Sell Stock"
date: 2020-03-06 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 121] Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## 문제 요약

각 날짜별로 주식의 가격을 나타내는 정수 배열이 주어졌을 때, 주식을 사고 팔아서 볼 수 있는 최대 이익을 구하는 문제.

## 풀이

배열을 순차적으로 탐색하며 주식의 최소 가격을 기록하고, 이후에 차익을 계산하며 최대 이익을 구한다.

## 코드

```Java
class Solution {
    public int maxProfit(int[] prices) {
        int ret = 0, min = prices[0];
        for (int i = 1; i < prices.length; i++) {
            ret = Math.max(ret, prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        return ret;
    }
}
```
