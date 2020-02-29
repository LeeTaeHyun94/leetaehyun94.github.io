---
layout: post
title:  "[LeetCode 27] Remove Element"
description:  "[LeetCode 27] Remove Element"
date:   2020-03-01 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 27] Remove Element](https://leetcode.com/problems/remove-element/)

## 문제 요약

정수형 배열과 특정 정수가 주어졌을 때, 배열 안의 특정 정수들을 제외하고 나머지 수들로 구성된 배열을 구하는 문제  
특이한 점은 추가 메모리 공간을 O(1)만큼만 사용할 것 (정수형 배열은 레퍼런스 형태로 전달되고 주어진 배열을 재구성하고 배열의 길이를 반환하면 된다.)

## 풀이

주어진 특정한 정수의 개수만큼 이전에 배열에 존재하는 다른 숫자들을 뒤로 보내주고, 다른 숫자들의 개수를 반환하면 된다.

## 코드

```Java
class Solution {
    public int removeElement(int[] nums, int val) {
        int gap = 0, len = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == val) gap++;
            else {
                nums[i - gap] = nums[i];
                len++;
            }
        }
        return len;
    }
}
```