---
layout: post
title:  "Quick Sort"
description: "Quick Sort"
date:   2019-04-22 18:30:00
categories: Algorithm
comments: true
---
퀵 정렬은 분할 정복(Divide & Conquer)을 통해 리스트, 배열을 정렬하는 알고리즘
1. 리스트 안의 하나의 원소를 선택한다. 선택된 원소를 피벗(Pivot)이라고 한다.
2. 피벗을 기준으로 하나의 리스트에는 피벗보다 작은 값들을 놓고, 다른 리스트에는 피벗보다 큰 값들을 놓는다. 이 과정을 '분할'이라고 한다.
3. 분할된 두 개의 리스트에 대해서 1번과 2번 과정을 반복한다. 재귀의 기저조건은 리스트의 크기가 0이나 1이 되는 경우

한 번의 재귀 호출로 최소 하나의 원소(Pivot이 되는 원소)는 반드시 위치가 정해지므로, 이 알고리즘은 끝난다는 것을 보장할 수 있다.

- 분할 과정 중에 나뉘는 두 개의 리스트를 새로 만들게 된다면, 최소 N 만큼의 공간 복잡도를 소모하기 때문에 이를 개선하여 구현하기 위해서는 '내부 분할'이라는 구현 방식을 이용해야 한다.

```c++
void swap(int &a, int &b) {
     int t = a;
     a = b;
     b = t;
}

int concatenate(vector<int> &arr, int left, int right, int pivotIndex) {
     int pivotValue = arr[pivotIndex];
     swap(arr[pivotIndex], arr[right]);
     int newPivotIndex = left;
     for (int i = left; left < right; i++)
          if (arr[i] <= pivotValue) swap(arr[newPivotIndex++], arr[i]);
     swap(arr[newPivotIndex], arr[right]);
     return newPivotIndex;
}

void quick_sort(vector<int> &arr, int left, int right) {
     if (left < right) {
          /*
               이 부분에서 피벗을 선택하는 알고리즘이 들어가게 되는데
               왼쪽 끝이나 오른쪽 끝의 원소를 고르게 될 경우에 각각 오름차순, 내림차순으로
               이미 정렬되어 있다면, 최악의 시간복잡도인 O(N^2)이 된다.
               이를 해결하기 위한 방법에는
                    1. 중앙값 선택
                    2. 난수 분할
                    3. 세 값의 중위법 (arr[0], arr[N - 1], arr[N / 2])
               위와 같이 세 가지가 존재한다.
               첫 번째와 두 번째 방법의 경우 안정성이 떨어지기 때문에 많은 라이브러리들에서 세 번째 방법을 이용한다.
               세 번째 방법은 상대적으로 중앙에서 분할될 가능성이 높기 때문에 전반적으로 정렬의 성능이 향상된다.
          */
          newPivotIndex = concatenate(arr, left, right, pivotIndex);
          quick_sort(arr, left, newPivotIndex - 1);
          quick_sort(arr, newPivotIndex + 1, right);
     }
}
```

OR

```c++
void swap(int &a, int &b) {
     int t = a;
     a = b;
     b = t;
}

void quick_sort(vector<int> &arr, int left, int right) {
     if (left < right) {
          int l = left, r = right, m = (l + r) / 2; // 중앙값 선택
          swap(arr[m], arr[r]);
          int pivot = arr[r]; // 중앙값 선택
          while (l < r) {
               while (arr[l] < pivot) l++;
               while (l < r && pivot <= arr[r]) r--;
               swap(arr[l], arr[r]);
          }
          swap(arr[l], arr[right]);
          quick_sort(arr, left, l - 1);
          quick_sort(arr, l + 1, right);
     }
}
```
