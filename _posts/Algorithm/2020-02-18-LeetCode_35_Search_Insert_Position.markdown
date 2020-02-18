---
layout: post
title: "[LeetCode 35] Search Insert Position"
description: "[LeetCode 35] Search Insert Position"
date: 2020-02-18 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 35] Search Insert Position](https://leetcode.com/problems/search-insert-position/)

## 문제 요약

정수 배열과 목표 정수가 주어졌을 때, 정수 배열 안에 목표 정수가 있다면 해당 위치의 인덱스를 반환하고 없다면 정수 배열의 오름차순 정렬을 유지하기 위해 목표 정수가 새롭게 위치해야 할 인덱스를 반환한다.

## 풀이

이진 탐색을 활용하면 간단하다.  
배열의 크기가 N이라면, 시간복잡도는 O(logN)이다.

## 코드

```Java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        while (l <= r) {
            int m = (l + r) / 2;
            if (nums[m] < target) l = m + 1;
            else r = m - 1;
        }
        return l;
    }
}
```