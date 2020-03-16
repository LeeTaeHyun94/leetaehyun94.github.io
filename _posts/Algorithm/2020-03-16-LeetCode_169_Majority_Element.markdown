---
layout: post
title: "[LeetCode 169] Majority Element"
description: "[LeetCode 169] Majority Element"
date: 2020-03-16 14:19:00
categories: Algorithm
comments: true
---
[[LeetCode 169] Majority Element](https://leetcode.com/problems/majority-element/)

## 문제 요약

배열의 크기가 n인 정수형 배열 하나가 주어졌을 때, 배열 안에서 Majority Element를 찾는 문제.  
Majority Element는 n / 2회보다 더 많이 나온 원소를 말한다.

## 풀이

HashMap 자료구조를 이용하여 각 원소가 몇 개 존재하는지 개수를 세어주었다.  
배열의 길이가 짝수이고 두 개의 원소가 각각 같은 횟수만큼 나왔을 때의 처리를 어떻게 해야할지 몰라 애매했지만, 그런 테스트케이스는 없던건지 AC를 받았다.  
실행 시간이 더 빠른 다른 사람의 답안을 봤는데 이런 식으로 풀 수도 있구나 싶어서 말문이 턱 막혔다.

## 코드

```Java
class Solution { // my 9ms solution
    public int majorityElement(int[] nums) {
        HashMap<Integer, Integer> hm = new HashMap<>();
        int l = nums.length;
        for (int i = 0; i < l; i++) {
            if (hm.containsKey(nums[i])) hm.put(nums[i], hm.get(nums[i]) + 1);
            else hm.put(nums[i], 1);
        }
        int ret = 0;
        for (int key : hm.keySet())
            if (l % 2 == 0 ? hm.get(key) >= l / 2 : hm.get(key) > l / 2) {
                ret = key;
                break;
            }
        return ret;
    }
}

class Solution { // the other's 0ms Solution
    public int majorityElement(int[] nums) {
        // return majority(nums);
        return backtrack(nums, nums[0], 0);
    }

    private int backtrack(int[] nums, int curr, int start){
        int count = 1;
        for(int i = start; i < nums.length; i++){
            if(nums[i] == curr)
                count++;
            else
                count--;
            if(count == 0)
                return backtrack(nums, nums[i], i + 1);
        }
        return curr;
    }
}
```
