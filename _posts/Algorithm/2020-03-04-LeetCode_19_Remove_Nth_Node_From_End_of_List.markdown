---
layout: post
title: "[LeetCode 19] Remove Nth Node From End of List"
description: "[LeetCode 19] Remove Nth Node From End of List"
date: 2020-03-04 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 19] Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

## 문제 요약

단방향 연결리스트와 자연수 n이 주어졌을 때, 뒤에서 n번째 노드를 삭제한 연결리스트를 반환하는 문제

## 풀이

재귀 함수를 이용하여 연결리스트의 맨 끝에 도달한 뒤, 반환을 통해 다시 되돌아 오면서 개수를 세어준다.  
노드의 개수와 n이 동일해지는 순간 다음 노드를 반환하고 그 다음 단계에서 다음 노드로의 연결을 반환된 노드로 이어준다.

## 코드

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    private int target;
    private int cnt = 0;
    
    private ListNode go(ListNode n) {
        if (n == null) {
            cnt++;
            return n;
        }
        ListNode tmp = go(n.next);
        if (cnt == target) {
            cnt++;
            return n.next;
        }
        if (cnt == target + 1) n.next = tmp;
        cnt++;
        return n;
    }
    
    public ListNode removeNthFromEnd(ListNode head, int n) {
        target = n;
        return go(head);
    }
}
```
