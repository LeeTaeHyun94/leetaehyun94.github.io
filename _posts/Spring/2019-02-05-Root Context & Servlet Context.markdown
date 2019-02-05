---
layout: post
title:  "Root Context & Servlet Context"
description: "Root Context & Servlet Context"
date:   2019-02-05 20:10:00
categories: Spring
comments: true
---
1. root-context (Root Application Context) : 전체 계층 구조에서 최상단에 위치한 context
   - 서로 다른 servlet context에서 공유해야 하는 Bean들을 정의. (ex. DataBase, Logging Setting etc..)
   - servlet context에 동일한 내용의 bean이 생기면 servlet context의 bean이 우선 적용된다.
   - 하나의 context에 정의된 AOP 설정은 다른 context에 영향을 미치지 않는다.
2.  servlet-context : 서블릿에서만 이용되는 context
   - 다른 servlet과 공유하기 위한 beans는 root-context에 정의하고 사용해야 한다.
   - DispatcherServlet은 자신만의 context를 생성, 초기화하고 root-context를 찾아서 parent context로 사용한다.