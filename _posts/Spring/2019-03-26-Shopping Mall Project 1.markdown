---
layout: post
title:  "Shopping Mall Project 1 - 작업 환경 설정"
description: "Shopping Mall Project 1 - 작업 환경 설정"
date:   2019-03-26 22:40:00
categories: Spring
comments: true
---
Spring MVC Project를 오래전에 해보고 Spring Boot만 사용하다보니 예전에 한 것들이 잘 기억나지 않아서 Shopping Mall 예제(https://kuzuro.blogspot.com/p/shopping-mall.html)를 보고 다시 감을 익히기로 했다.

블로그에 잘 정리가 되어 있어 우선은 블로그에 게시된 내용들을 따라해 본 다음, 원하는 기능을 추가하거나, 필요한 기능들만을 골라 Spring Boot 프로젝트로 RESTful API를 제공하고, React App을 만들 예정...

Ubuntu 18.04에서 작업했고, 이번 포스팅에서는 작업하는데 필요한 환경을 설정한다.

## 1. Tomcat 9 설치
(1) https://tomcat.apache.org/download-90.cgi 해당 링크에서 Core 파트의 tar.gz 파일을 다운받는다.

(2) 루트 디렉토리에 압축 해제

(3) cd /apache-tomcat-9.0.17/bin, sudo ./startup.sh 명령을 실행하여 tomcat 실행 확인

(4) sudo ./shutdown.sh : tomcat 중지

(5) sudo chmod -R 755 conf/ : conf 디렉토리의 권한 수정

## 2. Intellij에서 Spring MVC Project 생성하기
- Spring MVC + Maven

  (1) Spring MVC 를 선택하고 프로젝트명을 입력한후 프로젝트를 생성한다.

  (2) 좌측 project tree의 root directory를 우클릭 하여 Maven Framework를 추가한다.
  
  (3) Project Structure 창에서 Artifacts 탭을 클릭한다.

  (4) 우측의 이용 가능한 Library(Spring, Spring MVC)를 더블 클릭

- Run Configuration 설정

  (1) `+` 버튼을 누르고 Tomcat Server > Local 선택하고 이름을 설정

  (2) Server 탭의 Application server: `Configure...` 버튼을 클릭하고 Tomcat 설치한 디렉토리로 설정

  (3) Deployment 탭에서 Artifact 추가

여기까지 하면 Intellij에서 만든 Spring MVC Project가 Tomcat에서 실행이 되는 것을 확인할 수 있다.
