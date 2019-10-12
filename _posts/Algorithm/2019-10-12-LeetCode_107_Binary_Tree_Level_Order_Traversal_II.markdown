---
layout: post
title: "[LeetCode 107] Binary Tree Level Order Traversal II"
description: "[LeetCode 107] Binary Tree Level Order Traversal II"
date: 2019-10-12 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 107] Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

## 문제 요약

하나의 이진트리가 주어졌을 때, 주어진 트리의 높이 별로, 역순(단말노드->루트)으로 리스트에 원소를 저장하여 반환

## 풀이

재귀함수를 활용하여 트리의 순회하면서 트리의 최대 깊이를 기록하고, 기록된 높이만큼 리스트를 할당한다.  
트리에 대해 두 번째 순회를 진행하며 높이 별로 리스트에 원소를 추가한다.

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
    private List<List<Integer>> ret;
    private int tree_depth;
    
    private int chkDepth(TreeNode tn, int d) {
        if (tn == null) return d;
        return Math.max(chkDepth(tn.left, d + 1), chkDepth(tn.right, d + 1));
    }
    
    private void go(TreeNode tn, int d) {
        if (tn == null) return;
        ret.get(tree_depth - d - 1).add(tn.val);
        go(tn.left, d + 1);
        go(tn.right, d + 1);
    }
    
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        ret = new ArrayList<>();
        tree_depth = chkDepth(root, 0);
        for (int i = 0; i < tree_depth; i++) ret.add(new ArrayList<>());
        go(root, 0);
        return ret;
    }
}
```