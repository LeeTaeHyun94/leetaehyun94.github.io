---
layout: post
title:  "[LeetCode 26] Remove Duplicates from Sorted Array"
description:  "[LeetCode 26] Remove Duplicates from Sorted Array"
date:   2020-02-29 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 26] Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

## 문제 요약

오름차순으로 정렬된 정수형 배열이 주어졌을 때, 배열 안의 중복된 정수들을 각각 하나만 남기고 제외한 배열을 구하는 문제  
특이한 점은 추가 메모리 공간을 O(1)만큼만 사용할 것 (정수형 배열은 레퍼런스 형태로 전달되고 주어진 배열을 재구성하고 배열의 길이를 반환하면 된다.)

## 풀이

오름차순으로 정렬된 배열이 주어진다는 점을 이용해야 한다.  
그러므로 앞에서부터 순차적으로 배열을 확인하게 됐을 때 중복된 숫자라면 정렬되어 있는 상태이므로 반복해서 나오게 된다.  
이전에 나오는 숫자와 현재 새로 숫자를 저장해야 할 위치의 인덱스를 따로 저장한다. 그리고 현재 나오는 숫자와 이전에 나오는 숫자가 달라졌을 때 이전에 나온 숫자를 배열에 기록한 뒤 현재 새로 나온 숫자를 이전에 나오는 숫자로 갱신시켜 주며 배열을 순차적으로 확인해주면 된다.  
N이 배열의 길이라면, O(N)의 시간복잡도를 갖는다.
입력으로 빈 배열이 주어질 수도 있다는 점을 항상 유의하며 이처럼 엣지 케이스에 대한 경우를 고려해야 한다.

## 코드

```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length < 1) return 0;
        int len = 0, num = nums[0], idx = 0;
        for (int i = 1; i < nums.length; i++) {
            if (num != nums[i]) {
                nums[idx++] = num;
                num = nums[i];
                len++;
            }
        }
        nums[idx] = num;
        return len + 1;
    }
}
```