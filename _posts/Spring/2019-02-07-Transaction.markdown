---
layout: post
title:  "Transaction"
description: "Transaction"
date:   2019-02-07 10:13:00
categories: Spring
comments: true
---
하나의 업무에 여러 개의 작은 업무들이 같이 묶여 있는 것.

(ex. (게시글 추가, 포인트 적립), (댓글 추가, 댓글 숫자 업데이트))

* DB의 정규화와 트랜잭션은 서로 연관이 깊다. (정규화가 잘 돼 있을수록 연관 있는 데이터가 줄어들어 트랜잭션의 처리 또한 줄어든다.)
* Atomicity (원자성 - 트랜잭션은 하나의 단위로 처리), Consistency (일관성), Isolation (격리), Durability (영속성)

### 1. @Transactional

* Method > Class > Interface 순으로 트랜잭션 어노테이션 설정이 우선시 된다.