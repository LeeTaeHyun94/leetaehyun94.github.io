---
layout: post
title: "[LeetCode 104] Maximum Depth of Binary Tree"
description: "[LeetCode 104] Maximum Depth of Binary Tree"
date: 2019-10-11 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 104] Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

## 문제 요약

하나의 이진트리가 주어졌을 때, 주어진 트리의 최대 깊이(높이)를 구하는 문제

## 풀이

재귀함수를 활용하여 트리의 순회하면서 깊이를 기록한다.  

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
    public int go(TreeNode tn, int d) {
        if (tn == null) return d;
        return Math.max(go(tn.left, d + 1), go(tn.right, d + 1));
    }
    
    public int maxDepth(TreeNode root) {
        return go(root, 0);
    }
}
```