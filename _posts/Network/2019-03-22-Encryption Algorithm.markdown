---
layout: post
title:  "Encryption Algorithm"
description: "Encryption Algorithm"
date:   2019-03-22 20:40:00
categories: Network
comments: true
---
## 1. 암호화 알고리즘의 분류
![Encryption Algorithm](../../assets/Network/6.PNG)
가장 먼저 분류되는 방식은 양방향과 단방향 방식이다.

### (1) 양방향 알고리즘
암호화, 복호화 가능
- 대칭키(비공개키) 방식
  - ![대칭키 방식](../../assets/Network/7.PNG)
  - 특징 : 암호화, 복호화에 서로 동일한 키가 사용된다. 그래서 비공개키를 사용
  - 장점 : 속도가 빠르다.
  - 단점 : 송신 측에서 수신 측에 암호키를 전달하는 과정에서 노출의 우려가 있어 키 배송의 위험성이 있다.
  - ex : DES (Data Encryption Standard), AES
- 비대칭키(공개키) 방식
  - ![대칭키 방식](../../assets/Network/8.PNG)
  - 특징 : 암호화, 복호화에 서로 다른 키가 사용된다. 그래서 두 개의 키 중 하나의 키(비밀키/개인키)만 비밀로 보호하고 다른 하나의 키는 공개키로 사용한다.
  - 장점 : 키 배송의 위험성을 근본적으로 차단하여 안전성이 높다.
  - 단점 : 대칭키 방식에 비해 느리다.
  - ex : RSA

### (2) 단방향 알고리즘
- 암호문을 복호화하는 것이 불가능하다. (암호화만 가능)