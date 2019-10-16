---
layout: post
title: "[LeetCode 112] Path Sum"
description: "[LeetCode 112] Path Sum"
date: 2019-10-16 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 112] Path Sum](https://leetcode.com/problems/path-sum/)

## 문제 요약

이진트리와 정수 하나가 주어졌을 때, 트리의 루트부터 단말 노드까지 경로 상의 각 노드의 정수들의 합과 주어진 정수가 같은 경로가 있는지 확인하는 문제

## 풀이

재귀함수를 활용하여 트리를 순회하며 sum에서 현재 노드의 수만큼 빼주면서 단말 노드에 도달했을 때 sum이 0이 되는지를 확인

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        if (root.left == null)
            return (root.right == null) ? (sum - root.val == 0) : hasPathSum(root.right, sum - root.val);
        else
            return (root.right == null) ? hasPathSum(root.left, sum - root.val) : (hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val));
    }
}
```