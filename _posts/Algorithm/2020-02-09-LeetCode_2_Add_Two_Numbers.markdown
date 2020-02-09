---
layout: post
title: "[LeetCode 2] Add Two Numbers"
description: "[LeetCode 2] Add Two Numbers"
date: 2020-02-09 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 2] Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

## 문제 요약

두 양의 정수가 역순으로 이루어진 두 개의 연결리스트로 주어졌을 때, 이를 더하는 함수를 작성.

## 풀이

올림수와 연결리스트의 예외처리에 조금 신경써서 해주면 된다.  
올림수와 자릿수 연산을 할 때 나눗셈과 나머지 연산을 잘 사용하면 매우 유용하다.

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0), cur = head;
        int carry = 0;
        while (l1 != null && l2 != null) {
            int value = l1.val + l2.val + carry;
            cur.next = new ListNode(value % 10);
            carry = value / 10;
            l1 = l1.next;
            l2 = l2.next;
            cur = cur.next;
        }
        while (l1 != null) {
            int value = l1.val + carry;
            cur.next = new ListNode(value % 10);
            carry = value / 10;
            l1 = l1.next;
            cur = cur.next;
        }
         while (l2 != null) {
            int value = l2.val + carry;
            cur.next = new ListNode(value % 10);
            carry = value / 10;
            l2 = l2.next;
            cur = cur.next;
        }
        if (carry == 1) cur.next = new ListNode(1);
        return head.next;
    }
}
```