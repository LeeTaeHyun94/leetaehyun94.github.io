---
layout: post
title: "[LeetCode 155] Min Stack"
description: "[LeetCode 155] Min Stack"
date: 2019-10-22 17:56:00
categories: Algorithm
comments: true
---
[[LeetCode 155] Min Stack](https://leetcode.com/problems/min-stack/)

## 문제 요약

push(), pop(), top(), getMin()(스택 내의 최소 값을 구하는 메서드) 네 개의 메서드들이 상수 시간안에 동작하는 정수 자료형을 저장할 스택을 구성하는 문제

## 풀이

두 개의 스택으로 구성하는 방법, 연결리스트를 이용하여 헤드 노드에 현재 연결리스트 내의 최솟값을 저장하는 스택을 직접 만드는 방법 두 가지가 있다.  
두 개의 스택으로 구성하는 방법은 하나의 스택에는 단순하게 값을 삽입하고 다른 스택에는 현재까지 한 쪽 스택에 삽입된 값들 중 최솟값이 꼭대기에 오도록 값을 삽입한다.  
원소를 꺼낼 때는 최솟값이 빠져나갔는지를 확인해서 두 스택에서 모두 꺼내주면 된다.

## 코드

```Java
class MinStack { // v1
    Stack<Integer> stack, min_stack;

    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
        min_stack = new Stack<>();
    }
    
    public void push(int x) {
        stack.push(x);
        if (min_stack.empty() || min_stack.peek() >= x) min_stack.push(x);
    }
    
    public void pop() {
        if (stack.pop().equals(min_stack.peek())) min_stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min_stack.peek();
    }
}

class MinStack { // v2
    class Node {
        int val;
        int min;
        Node next;
        
        Node(int val) {
            this.val = val;
            min = val;
            next = null;
        }
        
        Node(int val, int min, Node next) {
            this.val = val;
            this.min = min;
            this.next = next;
        }
    }
    
    Node head;
    
    public void push(int x) {
        if (head == null) head = new Node(x);
        else head = new Node(x, Math.min(x, head.min), head);
    }
    
    public void pop() {
        head = head.next;
    }
    
    public int top() {
        return head.val;
    }
    
    public int getMin() {
        return head.min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
