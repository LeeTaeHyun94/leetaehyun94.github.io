---
layout: post
title: "[LeetCode 83] Remove Duplicates from Sorted List"
description: "[LeetCode 83] Remove Duplicates from Sorted List"
date: 2020-02-11 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 83] Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

## 문제 요약

정수 값이 오름차순으로 정렬된 연결리스트에서 중복 노드를 제거하는 문제

## 풀이

중복 노드를 제외하기 위해 이전의 값을 저장할 변수와 노드를 연결시키기 위한 지점을 저장할 변수 하나를 두고 구현한다.

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
    public ListNode deleteDuplicates(ListNode head) {
        if (head != null && head.next != null) {
            int num = head.val;
            ListNode pre = head, cur = head.next;
            while (cur != null) {
                if (cur.val != num) {
                    num = cur.val;
                    pre.next = cur;
                    pre = pre.next;
                }
                cur = cur.next;
            }
            pre.next = cur;
        }
        return head;
    }
}
```