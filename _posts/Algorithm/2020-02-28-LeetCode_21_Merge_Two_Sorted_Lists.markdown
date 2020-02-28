---
layout: post
title: "[LeetCode 21] Merge Two Sorted Lists"
description: "[LeetCode 21] Merge Two Sorted Lists"
date: 2020-03-01 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 21] Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

## 문제 요약

정수 데이터가 오름차순으로 저장된 두 개의 단방향 연결리스트가 주어졌을 때, 이 두 연결리스트를 하나의 연결리스트로 구성하여 해당 연결리스트의 헤드를 반환하는 문제

## 풀이

오름차순으로 정렬된 연결리스트가 주어진다는 점을 이용하여 하나의 연결리스트로 병합하는 방식은 머지 소트와 같은 방식으로 한다.  
l1과 l2의 첫 원소를 비교하여 시작점이 될 노드를 고른 후 이전에 확인한 노드를 제외하고 현재 l1과 l2의 첫 번째 노드를 각각 비교하여 더 작은 값을 갖는 노드를 현재 구성 중인 연결리스트의 뒤에 이어주는 방식으로 해결했다.  
이 문제에서는 새로운 연결리스트를 생성해도 무방했지만, 기존에 주어진 연결리스트만을 이용해야 하는 경우도 고려해봤다.  
또한, 연결리스트를 다루면서 null pointer exception이 발생할 수 있는데, 이를 여러 개의 조건문으로 예외처리하지 않고 코드를 간결하게 하는 방안에 대해서도 고심할 수 있었던 문제이다.  
각각 l1의 길이가 N, l2의 길이가 M이라면, O(N + M)의 시간복잡도를 갖는다.  
입력으로 빈 연결리스트(null)가 주어질 수도 있다는 점을 항상 유의하며 이처럼 엣지 케이스에 대한 경우를 고려해야 한다.

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
class Solution { // v1
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode ret;
        if (l1 == null && l2 == null) return null;
        else if (l1 == null) return l2;
        else if (l2 == null) return l1;
        if (l1.val > l2.val) {
            ret = new ListNode(l2.val);
            l2 = l2.next;
        }
        else {
            ret = new ListNode(l1.val);
            l1 = l1.next;
        }
        ListNode cur = ret;
        while (l1 != null || l2 != null) {
            int value;
            if (l1 != null && l2 != null) {
                if (l1.val > l2.val) {
                    value = l2.val;
                    l2 = l2.next;
                }
                else {
                    value = l1.val;
                    l1 = l1.next;
                }
            }
            else if (l1 == null) {
                value = l2.val;
                l2 = l2.next;
            }
            else {
                value = l1.val;
                l1 = l1.next;
            }
            cur.next = new ListNode(value);
            cur = cur.next;
        }
        return ret;
    }
}

class Solution { // v2
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}

class Solution { // v3
    public static ListNode go(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val < l2.val) {
            l1.next = go(l1.next, l2);
            return l1;
        }
        else {
            l2.next = go(l1, l2.next);
            return l2;
        }
    }
    
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        return go(l1, l2);
    }
}
```