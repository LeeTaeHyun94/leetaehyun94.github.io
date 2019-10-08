---
layout: post
title: "Unix System Programming"
description: "Unix System Programming"
date: 2019-10-08 18:40:00
categories: OS
comments: true
---
- Unix System Programming : 유닉스에서 제공하는 시스템 호출을 사용해 프로그램을 작성하는 것

- System Call
  - 응용 프로그램을 작성하는데에 유닉스 커널이 제공하는 서비스에 대한 프로그래밍 인터페이스
  - 기본적인 형태는 C언어의 함수와 같다.

- Library Function (`returned_value = system_call_name(parameters...);`)
  - Library : 미리 컴파일된 함수들을 묶어서 제공하는 특수한 형태의 파일
  - 자주 사용하는 기능을 독립적으로 분리하여 구현함으로써 프로그램의 개발과 디버깅을 쉽게 하고 컴파일을 더 빠르게 할 수 있다.
  - /lib, /usr/lib에 위치하며 lib*.a(정적 라이브러리) 또는 lib*.so(공유 라이브러리, 동적 실행시간(dynamic runtime shared library)) 형태로 제공

## 1. Compare System Call with Library Function
- 구조
  - System Call : 커널의 해당 서비스 모듈을 직접 호출하여 작업하고 결과를 리턴
  - Library Function : 일반적으로 커널 모듈을 직접 호출하지 않는다.
  - ![Compare System Call with Library Function](../../assets/OS/35.PNG)
- man 페이지 위치
  - System Call : 섹션 2
  - Library Function : 섹션 3
- 오류 처리 방법
  - System Call
    - 성공 시 0, 실패 시 1을 리턴
    - 전역 변수 errno에 오류 코드 저장 (man 페이지에서 코드 값 확인 가능)
  - Library Function : 섹션 3
    - 오류가 발생하면 NULL을 리턴, 함수의 리턴 값이 int 형이면 -1 리턴
    - errno에 오류 코드 저장

## 2. vi 편집기 명령
- 입력 모드 전환 : i, a, o, O
- 커서 이동 : 방향키 또는 j,h,k,l
- 한 글자 수정 : r
- 단어 수정 : cw
- 검색하여 수정 : `:%s/aaa/bbb/g`
- 붙이기 : p
- 글자 삭제 : x, #x(# : figure)
- 저장하고 종료 : `:wq!` 또는 ZZ
- 행 붙이기 : J
- 행 번호 보이기 : `:set nu`
- 명령 모드 전환 : ESC
- 행 이동 : #G(# : figure) 또는 `:line_number`
- 여러 글자 수정 : #s(# : figure)
- 명령 취소 : u, U
- 복사 : #yy(# : figure)
- 커서 이후 삭제 : D
- 행 삭제 (잘라내기) : dd, #dd(# : figure)
- 저장하지 않고 종료 : `:q!`
- 화면 다시 표시 : Ctrl + l
- 행 번호 없애기 : `:set nonu`