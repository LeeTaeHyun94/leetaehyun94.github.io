---
layout: post
title:  "Linked List"
description: "Linked List"
date:   2019-03-28 22:35:00
categories: Data_Structure
comments: true
---
```
#include<cstdio>
#include<algorithm>
#include<list>

using namespace std;

struct Node {
     int prev, next, val;
};

const int S = 30000, PUSH_BACK = 0, PUSH_FRONT = 1, INSERT = 2, POP_BACK = 3, POP_FRONT = 4, ERASE = 5;
int test_cmd[S][3];

void sw(Node &a, Node &b) {
     Node t = a;
     a = b;
     b = t;
}

struct MyList {
     int head = S, tail = S + 1, pos;
     Node nodes[S + 2];

     MyList() {
          pos = 0;
          nodes[head].prev = -1;
          nodes[head].next = tail;
          nodes[tail].prev = head;
          nodes[tail].next = -1;
     }

     void push_back(int data) {
          int prev = nodes[tail].prev, next = tail;
          nodes[pos].val = data;
          nodes[pos].prev = prev;
          nodes[pos].next = next;
          nodes[prev].next = pos;
          nodes[next].prev = pos++;
     }

     void push_front(int data) {
          int prev = head, next = nodes[head].next;
          nodes[pos].val = data;
          nodes[pos].prev = prev;
          nodes[pos].next = next;
          nodes[prev].next = pos;
          nodes[next].prev = pos++;
     }

     void insert(int idx, int data) {
          int prev = head;
          for (int i = 0; i < idx; prev = nodes[prev].next, i++);
          int next = nodes[prev].next;
          nodes[pos].val = data;
          nodes[pos].prev = prev;
          nodes[pos].next = next;
          nodes[prev].next = pos;
          nodes[next].prev = pos++;
     }

     void pop_back() {
          if (nodes[tail].prev == head) return;
          int target = nodes[tail].prev, prev = nodes[target].prev;
          nodes[tail].prev = prev
          nodes[prev].next = tail;
          if (--pos == target) return;
          int swprev = nodes[pos].prev, swnext = nodes[pos].next;
          nodes[swprev].next = nodes[swnext].prev = target;
          sw(nodes[pos], nodes[target]);
     }

     void pop_front() {
          if (nodes[head].next == tail) return;
          int target = nodes[head].next, next = nodes[target].next;
          nodes[head].next = next;
          nodes[next].prev = head;
          if (--pos == target) return;
          int swprev = nodes[pos].prev, swnext = nodes[pos].next;
          nodes[swprev].next = nodes[swnext].prev = target;
          sw(nodes[pos], nodes[target]);
     }

     void erase(int idx) {
          int prev = head;
          for (int i = 0; i < idx; prev = nodes[prev].next, i++)
               if (nodes[prev].next == tail) return;
          int target = nodes[prev].next, next = nodes[target].next;
          nodes[prev].next = next;
          nodes[next].prev = prev;
          if (--pos == target) return;
          int swprev = nodes[pos].prev, swnext = nodes[pos].next;
          nodes[swprev].next = nodes[swnext].prev = target;
          sw(nodes[pos], nodes[target]);
     }
} my_list;

list<int> stl_list;

int main() {
	int cur_size = 0;
	for (int i = 0; i < S; i++) {
		if (i < S / 3) test_cmd[i][0] = rand() % 2;
		else test_cmd[i][0] = rand() % 6;
		switch (test_cmd[i][0])
		{
		case PUSH_BACK:
		case PUSH_FRONT:
			test_cmd[i][1] = rand();
			cur_size++;
			break;
		case INSERT:
			test_cmd[i][1] = rand() % cur_size;
			test_cmd[i][2] = rand();
			cur_size++;
			break;
		case POP_BACK:
		case POP_FRONT:
			cur_size--;
			break;
		case ERASE:
			test_cmd[i][1] = rand() % cur_size;
			cur_size--;
			break;
		}
	}
	int my_list_begin = GetTickCount();
	for (int i = 0; i < S; i++) {
		switch (test_cmd[i][0])
		{
		case PUSH_BACK: my_list.push_back(test_cmd[i][1]); break;
		case PUSH_FRONT: my_list.push_front(test_cmd[i][1]); break;
		case INSERT: my_list.insert(test_cmd[i][1], test_cmd[i][2]); break;
		case POP_BACK: my_list.pop_back(); break;
		case POP_FRONT: my_list.pop_front(); break;
		case ERASE: my_list.erase(test_cmd[i][1]); break;
		}
	}
	int my_list_end = GetTickCount(), stl_list_begin = GetTickCount();
	for (int i = 0; i < S; i++) {
		switch (test_cmd[i][0])
		{
		case PUSH_BACK: stl_list.push_back(test_cmd[i][1]); break;
		case PUSH_FRONT: stl_list.push_front(test_cmd[i][1]); break;
		case INSERT: {
			list<int>::iterator it = stl_list.begin();
			for (int j = 0; j < test_cmd[i][1]; j++, it++);
			stl_list.insert(it, test_cmd[i][2]);
			break;
		}
		case POP_BACK: stl_list.pop_back(); break;
		case POP_FRONT: stl_list.pop_front(); break;
		case ERASE: {
			list<int>::iterator it = stl_list.begin();
			for (int j = 0; j < test_cmd[i][1]; j++, it++);
			stl_list.erase(it);
			break;
		}
		}
	}
	int stl_list_end = GetTickCount();
	puts("Compare execution time");
	printf("My List : %d\n", my_list_end - my_list_begin);
	printf("STL List : %d\n", stl_list_end - stl_list_begin);
	list<int>::iterator it = stl_list.begin();
	int cur = my_list.node[my_list.head].next;
	while (it != stl_list.end()) {
		if (*it != my_list.node[cur].val) puts("Error");
		++it;
		cur = my_list.node[cur].next;
	}
	return 0;
}
```