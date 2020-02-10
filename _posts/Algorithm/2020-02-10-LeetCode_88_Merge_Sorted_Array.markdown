---
layout: post
title: "[LeetCode 88] Merge Sorted Array"
description: "[LeetCode 88] Merge Sorted Array"
date: 2020-02-10 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 88] Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

## 문제 요약

오름차순으로 정렬된 정수 배열 두 개가 주어졌을 때, 이 두 배열을 하나의 정렬된 배열로 만드는 문제.

## 풀이

병합 정렬의 병합 과정과 구현이 같다.

## 코드

```Java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int temp[] = new int[m];
        for (int i = 0; i < m; i++) temp[i] = nums1[i];
        int idx = 0, a = 0, b = 0;
        while (a < m && b < n) nums1[idx++] = temp[a] < nums2[b] ? temp[a++] : nums2[b++];
        while (a < m) nums1[idx++] = temp[a++];
        while (b < n) nums1[idx++] = nums2[b++];
    }
}
```