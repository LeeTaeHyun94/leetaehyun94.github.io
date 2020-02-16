---
layout: post
title: "[LeetCode 53] Maximum Subarray"
description: "[LeetCode 53] Maximum Subarray"
date: 2020-02-16 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 53] Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

## 문제 요약

정수 배열이 주어졌을 때, 연속된 부분 배열의 합 중 최대 값을 구하는 문제

## 풀이

포인트는 연속된 부분 배열의 합이라는 것이다.  
연속된 부분 배열의 합을 구하는 방법에는 누적합 배열을 구성하는 것만큼 간단한 방법이 없다.  
누적합 배열이란, O(N)의 전처리를 통해 배열의 각 구간 별로 누적합을 O(1)만에 구할 수 있는 방법이다.  
누적합 배열을 구성하는 방법은 간단하다. 주어진 정수형 배열을 순차적으로 탐색하며 이전 인덱스까지의 누적합에 현재 탐색 중인 정수를 더하며 구성하면 된다.  
이 아이디어에서 조금 더 발전시켜보면, 이 문제를 간단히 해결할 수 있는 방법이 떠오른다.  
결국 최대값이 되기 위한 연속된 부분 배열의 합은 가장 큰 누적합과 가장 작은 누적합을 구한 뒤 뺀 값이 될 수 밖에 없다. (인덱스는 당연히 가장 큰 누적합 부분이 작아야 한다.)  
따라서 나는 누적합을 구하면서 동시에 가장 작은 누적합을 갱신시키고 현재 누적합 값에서 이전에 나왔던 가장 작은 누적합 값을 빼서 최댓값을 구했다.

## 코드

```Java
class Solution {
    public int maxSubArray(int[] nums) {
        int sums  = 0, ret = Integer.MIN_VALUE, min = 0;
        for (int i = 0; i < nums.length; i++) {
            sums += nums[i];
            int res = sums - min;
            if (ret < res) ret = res;
            if (min > sums) min = sums;
            /*
                ret = Math.max(ret, res);
                min = Math.min(min, sums);
            */
        }
        return ret;
    }
}
```