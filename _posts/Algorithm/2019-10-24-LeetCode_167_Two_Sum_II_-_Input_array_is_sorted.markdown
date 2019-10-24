---
layout: post
title: "[LeetCode 167] Two Sum II - Input array is sorted"
description: "[LeetCode 167] Two Sum II - Input array is sorted"
date: 2019-10-24 20:23:00
categories: Algorithm
comments: true
---
[[LeetCode 167] Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

## 문제 요약

오름차순으로 정렬된 정수형 배열과 목표가 될 정수 하나가 주어졌을 때, 합하여 목표 정수를 만드는 두 개의 정수(두 정수의 배열 인덱스)를 구하는 문제

## 풀이

처음에는 생각을 짧게 하여, 반복문으로 정수를 하나씩 탐색하며, 나머지 다른 정수를 정렬된 배열 안에서 이진탐색으로 찾아내는 방법을 사용하였다.  
더 간단한 방법은 왼쪽 끝과 오른쪽 끝에서 시작하여 두 인덱스가 가리키는 정수를 합했을 때, 목표치보다 작다면 왼쪽 끝에서 한 칸 오른쪽으로 움직이고, 목표치보다 크다면 오른쪽 끝에서 한 칸 왼쪽으로 움직여주면 훨씬 효율적으로 찾을 수 있다. (투 포인터)

## 코드

```Java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int l = 0, r = numbers.length - 1;
        int[] ans = new int[2];
        while (l <= r) {
            int t = numbers[l] + numbers[r];
            if (t < target) l++;
            else if (t > target) r--;
            else {
                ans[0] = l + 1;
                ans[1] = r + 1;
                break;
            }
        }
        return ans;
    }
}
```
