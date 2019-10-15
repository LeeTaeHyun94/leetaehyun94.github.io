---
layout: post
title: "[LeetCode 111] Minimum Depth of Binary Tree"
description: "[LeetCode 111] Minimum Depth of Binary Tree"
date: 2019-10-15 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 111] Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

## 문제 요약

이진트리가 주어졌을 때, 트리의 최소 깊이를 구하는 문제  
최소 깊이 = 루트와 루트로부터 가장 가까운 단말 노드 간의 최단 경로 안에 있는 노드의 개수

## 풀이

재귀함수를 활용하여 트리를 순회하며 반환 시점에 단말 노드에서부터 깊이를 1씩 더해주면서 깊이의 최솟값을 구한다.

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
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        if (root.left == null)
            return root.right == null ? 1 : minDepth(root.right) + 1;
        else
            return (root.right == null ? minDepth(root.left) : Math.min(minDepth(root.left), minDepth(root.right))) + 1;
    }
}
```