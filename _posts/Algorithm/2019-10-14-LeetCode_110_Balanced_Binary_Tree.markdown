---
layout: post
title: "[LeetCode 110] Balanced Binary Tree"
description: "[LeetCode 110] Balanced Binary Tree"
date: 2019-10-14 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 110] Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

## 문제 요약

이진트리가 주어졌을 때, 균형잡힌 이진트리인지 판별하는 문제

## 풀이

재귀함수를 활용하여 트리를 순회하며 왼쪽 서브트리의 깊이와 오른쪽 서브트리의 깊이 차이가 2 이상 나는 것을 확인해준다.

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
    private boolean ret = true;
    
    private int go(TreeNode tn, int d) {
        if (tn == null) return d;
        int ld = go(tn.left, d + 1), rd = go(tn.right, d + 1);
        if (Math.abs(ld - rd) > 1) ret = false;
        return Math.max(ld, rd);
    }
    
    public boolean isBalanced(TreeNode root) {
        go(root, 0);
        return ret;
    }
}
```