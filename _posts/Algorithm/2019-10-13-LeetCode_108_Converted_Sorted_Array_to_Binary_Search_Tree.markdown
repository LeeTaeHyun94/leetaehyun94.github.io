---
layout: post
title: "[LeetCode 108] Convert Sorted Array to Binary Search Tree"
description: "[LeetCode 108] Convert Sorted Array to Binary Search Tree"
date: 2019-10-13 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 108] Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

## 문제 요약

오름차순으로 정렬된 정수 배열이 주어졌을 때, 해당 데이터를 균형잡힌 이진트리로 구현하는 문제

## 풀이

재귀함수를 활용하여 배열의 중간값이 현재 서브트리의 루트에 와야 한다는 것이 포인트  
또한, 중간값을 기준으로 왼쪽의 원소들은 서브트리의 또 다른 왼쪽 서브트리가 되고 오른쪽의 원소들은 오른쪽 서브트리로 구성된다.

## 코드

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private TreeNode go(int[] nums, int l, int r) {
        if (l > r) return null;
        int m = (l + r) / 2;
        TreeNode root = new TreeNode(nums[m]);
        root.left = go(nums, l, m - 1);
        root.right = go(nums, m + 1, r);
        return root;
    }
    
    public TreeNode sortedArrayToBST(int[] nums) {
        return go(nums, 0, nums.length - 1);
    }
}
```