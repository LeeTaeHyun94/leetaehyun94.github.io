---
layout: post
title: "[LeetCode 176] Second Highest Salary"
description: "[LeetCode 176] Second Highest Salary"
date: 2020-03-13 21:08:00
categories: Algorithm
comments: true
---
[[LeetCode 176] Second Highest Salary](https://leetcode.com/problems/second-highest-salary/)

## 문제 요약

Salary 정보가 들어있는 Employee 테이블이 주어졌을 때, 두 번째로 높은 Salary를 찾는 SQL 문제

## 풀이

SQL을 잘 알지 못해서 두 번째 Row를 구하는 두 가지 방법을 찾을 수 있었다.  
첫 번째는 limit과 offset을 이용한 방법인데, limit n offset m이라면, m번째부터 n개의 Row를 반환한다. 보통 paging 알고리즘에 이용된다. (+ distinct를 활용하여 중복도 제거해주어야 한다.)  
두 번째는 max 함수를 이용하여 서브쿼리로 최댓값을 뽑고 이 Salary보다 작은 것들 중에서 최댓값을 구하면 된다.  
주의해야 할 점은 Salary가 모두 같거나, 하나 밖에 없을 때 두 번째로 높은 Salary는 존재하지 않는데, 이 때 null을 반환해야 한다.  
SQL에서 null 처리를 어떤 방식으로 하는지 생각하고 찾아봐야 할 것 같다. (ifnull이라는 함수도 있었다.)

## 코드

```SQL
# v1
select
    (select distinct Salary
    from Employee
    order by Salary desc
    limit 1 offset 1) SecondHighestSalary;

# v2 
select max(Salary) SecondHighestSalary
from Employee
where Salary < (select max(Salary) from Employee);
```
