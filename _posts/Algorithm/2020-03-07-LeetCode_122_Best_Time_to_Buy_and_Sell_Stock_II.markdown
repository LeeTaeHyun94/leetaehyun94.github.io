---
layout: post
title: "[LeetCode 122] Best Time to Buy and Sell Stock II"
description: "[LeetCode 122] Best Time to Buy and Sell Stock II"
date: 2020-03-07 17:06:00
categories: Algorithm
comments: true
---
[[LeetCode 122] Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

## 문제 요약

각 날짜별로 주식의 가격을 나타내는 정수 배열이 주어졌을 때, 주식을 가능한 여러 번 사고 팔아서 볼 수 있는 최대 이익을 구하는 문제.

## 풀이

가능한 많은 거래 횟수를 통해 최대 이익을 내기 위해서는 가격이 낮은 날에 사서 가격이 오르다가 떨어지기 직전에 파는 행위를 반복해야 한다.  
주식의 가격을 그래프로 그려 생각해 보면, 마치 /^ 이런 모양의 지점마다 사고 팔고를 반복한다는 의미이다.  
그러므로 배열을 순차적으로 탐색하며 주식을 사기 위한 최소 가격을 기록하고 현재 인덱스 직전의 주식 가격을 기록해서 가격이 떨어지는 날을 만났을 때 그 전날이 당시 최고 가격을 의미하므로 전날의 주식 가격과 최소 주식 가격의 차익을 더해주면서 최대 이익을 구한다.  
유의해야 할 점은 정수 배열이 비어있을 때, 배열을 순차적으로 탐색하며 확인해야 할 순서는 가장 먼저 주식을 팔아서 이득을 볼 수 있는지를 확인(이득을 봤다면 그 전날 주식을 팔아야 했다는 것이므로 주식의 최소 가격은 오늘 가격으로 갱신)하고 그 다음 주식의 최소 가격을 기록하는 것이고 마지막으로 전 날의 주식 가격을 갱신해주는 것이다.

## 코드

```Java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length < 1) return 0;
        int pre = prices[0], buy_price = prices[0], ret = 0;
        for (int i = 1; i < prices.length; i++) {
            if (pre > prices[i]) {
                ret += pre - buy_price;
                buy_price = prices[i];
            }
            buy_price = Math.min(buy_price, prices[i]);
            pre = prices[i];
        }
        if (pre - buy_price > 0) ret += pre - buy_price;
        return ret;
    }
}
```
