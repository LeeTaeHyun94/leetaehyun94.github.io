---
layout: post
title: "[LeetCode 160] Intersection of Two Linked Lists"
description: "[LeetCode 160] Intersection of Two Linked Lists"
date: 2019-10-23 20:19:00
categories: Algorithm
comments: true
---
[[LeetCode 160] Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

## 문제 요약

두 개의 연결리스트가 주어졌을 때, 두 연결리스트의 교차점을 구하는 문제

## 풀이

각 연결리스트의 노드 개수를 세어 더 많은 노드를 가진 쪽의 연결리스트를 앞으로 진행시켜 노드의 개수를 똑같이 맟춰준다.  
그 다음, 두 연결리스트 모두 앞으로 하나씩 진행시켜 주면서 주소 값이 같은지를 비교하여 같다면 교차점, 같지 않다면 교차점이 아니라는 것이다.  

## 코드

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode A = headA, B = headB;
        int a = 0, b = 0;
        while (A != null) {
            a++;
            A = A.next;
        }
        while (B != null) {
            b++;
            B = B.next;
        }
        A = a > b ? headA : headB;
        B = a > b ? headB : headA;
        for (int i = 0; i < Math.abs(a - b); i++) A = A.next;
        for (; A != null; A = A.next, B = B.next)
            if (A == B) return A;
        return null;
    }
}
```
