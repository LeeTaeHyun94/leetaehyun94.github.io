---
layout: post
title: "[LeetCode 146] LRU Cache"
description: "[LeetCode 146] LRU Cache"
date: 2020-03-05 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 146] LRU Cache](https://leetcode.com/problems/lru-cache/)

## 문제 요약

LRU(Least Recently Used) Cache를 구현하는 문제.  
(LRUCache 클래스의 생성자와 get, put 함수 구현)

## 풀이

실제 key, value 데이터는 HashMap 자료구조를 통해 저장하는데, 이 때 HashMap의 value에는 이중 연결리스트의 노드를 저장한다.  
이중 연결리스트를 이용하여 get과 put 연산 시에 사용 순서를 갱신한다. 오래된 노드는 tail에서 삭제하고, 최근 사용된 노드는 head에 추가한다.

## 코드

```Java
class LRUCache {
    private class ListNode {
        private int val;
        private int key;
        private ListNode prev;
        private ListNode next;
        
        private ListNode(int key, int val) {
            this.key = key;
            this.val = val;
            this.prev = null;
            this.next = null;
        }
    }
    
    private void insert(ListNode n) {
        head.next.prev = n;
        n.next = head.next;
        n.prev = head;
        head.next = n;
    }
    
    private void delete(ListNode n) {
        n.prev.next = n.next;
        n.next.prev = n.prev;
    }
    
    private HashMap<Integer, ListNode> cache;
    private int capacity;
    private int cur_cap;
    private ListNode head;
    private ListNode tail;

    public LRUCache(int capacity) {
        cache = new HashMap<>();
        this.capacity = capacity;
        cur_cap = 0;
        head = new ListNode(0, 0);
        tail = new ListNode(0, 0);
        head.prev = tail;
        head.next = tail;
        tail.next = head;
        tail.prev = head;
    }
    
    public int get(int key) {
        if (cache.containsKey(key)) {
            ListNode n = cache.get(key);
            delete(n);
            insert(n);
            return n.val;
        }
        else return -1;
    }
    
    public void put(int key, int value) {
        ListNode new_node = new ListNode(key, value);
        if (cache.containsKey(key)) {
            ListNode old_node = cache.get(key);
            delete(old_node);
            cache.remove(old_node.key);
        }
        else {
            if (cur_cap >= capacity) {
                ListNode old_node = tail.prev;
                delete(old_node);
                cache.remove(old_node.key);
            }
            cur_cap++;
        }
        insert(new_node);
        cache.put(key, new_node);
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
