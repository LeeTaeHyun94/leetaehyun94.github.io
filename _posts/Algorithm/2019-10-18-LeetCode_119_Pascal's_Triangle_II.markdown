---
layout: post
title: "[LeetCode 119] Pascal's Triangle II"
description: "[LeetCode 119] Pascal's Triangle II"
date: 2019-10-17 18:30:00
categories: Algorithm
comments: true
---
[[LeetCode 119] Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/)

## 문제 요약

파스칼의 삼각형 구현, 입력으로 주어진 행에 대해서만 출력하면 된다.

## 풀이

파스칼의 삼각형 구현이지만, 입력으로 주어진 행에 대해서만 반환하면 되므로 메모리를 절약하는 것에 초점을 맞춘 문제이다.  
k = rowIndex일 때, O(k)만큼의 공간복잡도만을 사용해야 할 경우 파스칼의 삼각형 배열을 앞에서부터 채우지 않고 뒤에서부터 채워주고 끝에 1을 추가해주는 방식을 사용한다.  
추가적으로 자바에서는 직접 ArrayList를 다루는 것보다 배열을 만든 다음, 이를 List로 변환해주는 것이 근소하게 효율적(시공간 복잡도 측면)이다.  
주의할 점 : Arrays.fill() 메서드로 배열에 값이 있어야 한다는 점, Arrays.asList() 메서드를 기억하고 있어야 한다는 점

## 코드

```Java
class Solution { // v1
    public List<Integer> getRow(int rowIndex) {
        List<Integer> pre, cur = new ArrayList<>();
        cur.add(1);
        if (rowIndex < 1) return cur;
        cur.add(1);
        if (rowIndex < 2) return cur;
        for (int i = 2; i <= rowIndex; i++) {
            pre = cur;
            cur = new ArrayList<>();
            cur.add(1);
            for (int j = 1; j < i; j++) cur.add(pre.get(j - 1) + pre.get(j));
            cur.add(1);
        }
        return cur;
    }
}

class Solution { // v2
    public List<Integer> getRow(int rowIndex) {
        List<Integer> ret = new ArrayList<>();
        ret.add(1);
        for (int i = 1; i <= rowIndex; i++) {
            for (int j = i - 1; j > 0; j--)
                ret.set(j, ret.get(j - 1) + ret.get(j));
            ret.add(1);
        }
        return ret;
    }
}

class Solution { // v3
    public List<Integer> getRow(int rowIndex) {
        Integer[] dp = new Integer[rowIndex + 1];
        Arrays.fill(dp, 0);
        dp[0] = 1;
        for (int i = 1; i <= rowIndex; i++) {
            for (int j = i; j > 0; j--) dp[j] += dp[j - 1];
        }
        return Arrays.asList(dp);
    }
}
```