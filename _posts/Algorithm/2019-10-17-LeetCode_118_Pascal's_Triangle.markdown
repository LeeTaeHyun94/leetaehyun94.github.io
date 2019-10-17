---
layout: post
title: "[LeetCode 118] Pascal's Triangle"
description: "[LeetCode 118] Pascal's Triangle"
date: 2019-10-17 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 118] Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)

## 문제 요약

파스칼의 삼각형 구현

## 풀이

주어지는 행의 개수에 유의하여 파스칼의 삼각형을 구현해주면 된다.

## 코드

```Java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ret = new ArrayList<>();
        if (numRows == 0) return ret;
        ret.add(new ArrayList<>());
        ret.get(0).add(1);
        if (numRows == 1) return ret;
        ret.add(new ArrayList<>());
        ret.get(1).add(1);
        ret.get(1).add(1);
        for (int i = 2; i < numRows; i++) {
            ret.add(new ArrayList<>());
            ret.get(i).add(1);
            for (int j = 1; j < i; j++)
                ret.get(i).add(ret.get(i - 1).get(j - 1) + ret.get(i - 1).get(j));
            ret.get(i).add(1);
        }
        return ret;
    }
}
```