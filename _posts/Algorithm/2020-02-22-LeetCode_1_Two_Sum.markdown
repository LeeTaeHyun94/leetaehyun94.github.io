---
layout: post
title: "[LeetCode 1] Two Sum"
description: "[LeetCode 1] Two Sum"
date: 2020-02-22 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 1] Two Sum](https://leetcode.com/problems/two-sum/)

## 문제 요약

정수 배열과 목표 합이 주어졌을 때, 정수 배열 안에서 목표 합을 만들 수 있는 두 정수의 각 인덱스를 구하는 문제.  
반드시 하나의 정답은 있다.

## 풀이

(v1) 2중 for문으로 모든 경우의 수를 확인하는 방법  (O(N^2))
(v2) 주어진 정수와 인덱스를 짝지어 Key-Value 형태의 자료구조인 HashMap에 저장하여 어느 한 쪽의 정수를 특정하였을 때, 나머지 짝이 될 수 있는 정수를 HashMap에서 찾는 방법 (O(N))  
(v3) 2번의 풀이에서도 시간복잡도를 아끼는 방법이 있는데, 처음에 배열을 모두 돌아 HashMap을 구성하는 것이 아니라 배열을 탐색하면서 바로 나머지 짝이 될 수 있는 정수를 HashMap에서 찾아보고 없다면 HashMap에 현재 보고있는 정수를 저장한다.  
    -> 이는 현재 보고있는 정수가 이후에 배열을 마저 탐색하면서 나머지 짝이 될 수 있는 가능성이 있기 때문이다. 다시 말해 HashMap의 구성과 어느 한쪽의 정수를 특정하는 과정을 동시에 하는 것이라고 볼 수 있다.

## 코드

```Java
class Solution { // v1
    public int[] twoSum(int[] nums, int target) {
        int[] ret = new int[2];
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (i == j) continue;
                if (nums[i] + nums[j] == target) {
                    ret[0] = i;
                    ret[1] = j;
                }
            }
        }
        return ret;
    }
}

class Solution { // v2
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> nums_and_idxs = new HashMap<>();
        int[] ret = new int[2];
        for (int i = 0; i < nums.length; i++) nums_and_idxs.put(nums[i], i);
        for (int i = 0; i < nums.length; i++) {
            int A = target - nums[i];
            if (nums_and_idxs.containsKey(A)) {
                int B_idx = nums_and_idxs.get(A);
                if (B_idx == i) continue;
                ret[0] = i;
                ret[1] = B_idx;
                return ret;
            }
        }
        return ret;
    }
}

class Solution { // v3
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> nums_and_idxs = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int A = nums[i], B = target - A;
            if (nums_and_idxs.containsKey(B)) {
                return new int[]{i, nums_and_idxs.get(B)};
            }
            nums_and_idxs.put(A, i);
        }
        return new int[2];
    }
}
```