---
layout: post
title: "[LeetCode 141] Linked List Cycle"
description: "[LeetCode 141] Linked List Cycle"
date: 2019-10-21 17:36:00
categories: Algorithm
comments: true
---
[[LeetCode 141] Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

## 문제 요약

단방향 연결 리스트가 주어졌을 때, 연결 리스트 내에 사이클이 존재하는지 판별하는 문제

## 풀이

연결 리스트의 노드 별로 방문 여부를 체크하는 가장 단순한 방법이 있다.  
하지만, 이 방법은 연결 리스트의 노드 개수(크기)만큼 공간복잡도를 사용한다.  
O(1)만큼의 공간복잡도를 사용하기 위한 방법은 리스트 노드를 가리키는 두 개의 변수를 선언하고 한 개는 한 칸씩, 다른 하나는 두 칸씩 움직인다.  
만약 사이클이 존재한다면, 한 칸씩 앞으로 가는 변수와 두 칸씩 앞으로 가는 변수가 만나는 지점이 존재한다.  
사이클이 존재하지 않는다면, 두 변수는 만날 일이 없다. 결국 연결 리스트의 끝을 의미하는 null을 만나게 된다.  
중간 중간 NullPointerException이 있을 수 있으므로 예외 처리를 잘 해주어야 한다.

## 코드

```Java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;
        ListNode l1 = head, l2 = head;
        do {
            l1 = l1.next;
            l2 = l2.next;
            if (l1 == null || l2 == null) return false;
            l2 = l2.next;
            if (l2 == null) return false;
        } while (l1 != l2);
        return true;
    }
}
```
