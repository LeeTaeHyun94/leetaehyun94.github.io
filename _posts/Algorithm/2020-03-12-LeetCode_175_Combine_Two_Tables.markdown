---
layout: post
title: "[LeetCode 175] Combine Two Tables"
description: "[LeetCode 175] Combine Two Tables"
date: 2020-03-12 20:40:00
categories: Algorithm
comments: true
---
[[LeetCode 175] Combine Two Tables](https://leetcode.com/problems/combine-two-tables/)

## 문제 요약

두 테이블이 주어졌을 때, 두 테이블을 조인한 결과를 구하는 SQL 문제

## 풀이

각 사람 별로 주소가 있는지 여부에 관계없이 조인하는 문제이므로, Person이 왼쪽에 있다는 기준으로 LEFT OUTER JOIN을 해주면 된다.

## 코드

```SQL
# Write your MySQL query statement below
select FirstName, LastName, City, State
from Person
    left outer join Address
    on Person.PersonId = Address.PersonId;
```
