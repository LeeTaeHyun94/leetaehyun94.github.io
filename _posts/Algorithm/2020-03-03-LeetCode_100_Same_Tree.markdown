---
layout: post
title: "[LeetCode 100] Same Tree"
description: "[LeetCode 100] Same Tree"
date: 2020-03-03 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 100] Same Tree](https://leetcode.com/problems/same-tree/)

## 문제 요약

두 개의 트리가 주어졌을 때, 트리가 같은지를 판별하는 문제.

## 풀이

재귀함수를 활용하여 트리의 순회 순서를 결정하고 트리가 서로 같은지를 판별한다.

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null) return q == null ? true : false;
        if (q == null) return false;
        if (p.val != q.val) return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```