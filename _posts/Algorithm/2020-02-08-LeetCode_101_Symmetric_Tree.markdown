---
layout: post
title: "[LeetCode 101] Symmetric Tree"
description: "[LeetCode 101] Symmetric Tree"
date: 2020-02-08 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 101] Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

## 문제 요약

하나의 이진트리가 주어졌을 때, 주어진 트리가 대칭인지를 판별하는 문제.

## 풀이

재귀함수를 활용하여 트리의 순회 순서를 결정하고 트리가 서로 대칭인지를 판별한다.  
(대칭이 되기 위한 비교 대상은 트리의 왼쪽 서브트리의 왼쪽 자식과 오른쪽 서브트리의 오른쪽 자식 / 왼쪽 서브트리의 오른쪽 자식과 오른쪽 서브트리의 왼쪽 자식)

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
    private boolean go(TreeNode l, TreeNode r) {
        if (l == null && r == null) return true;
        if (l == null || r == null) return false;
        return l.val == r.val && go(l.left, r.right) && go(l.right, r.left);
    }
    
    public boolean isSymmetric(TreeNode root) {
        return root == null ? true : go(root.left, root.right);
    }
}
```