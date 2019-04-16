---
layout: post
title:  "Programming Paradigm"
description: "Programming Paradigm"
date:   2019-04-16 23:48:00
categories: Programming_Languages
comments: true
---
- 패러다임

  - 계산의 본질을 보는 관점에 따라 프로그래밍 언어를 분류
  - 명령형 언어, 함수 언어, 논리 언어, 객체지향 언어

- 명령형 언어

  - 폰 노이만 구조라 불리는 컴퓨터 구조를 기반

    - 명령의 순차적인 실행, 메모리 위치를 의미하는 변수의 사용, 변수의 값을 바꾸는 배정문의 사용

    - 변수 x와 y를 사용하고, 배정문 '='를 사용하며, 위에서부터 아래로 순차적으로 실행

      - ```c
        int main(void) {
            int x, y;
            x = 10;
            y = x + 20;
            return 0;
        }
        ```

- 함수 언어

  - 수학 함수와 같은 원리의 함수들로 프로그램을 구성

  - 변수, 배정문 등을 사용하지 않는다.

  - LISP

    - ```lisp
      (first (sort '(3 9 7 5)))
      // first와 sort는 함수로 미리 정의되어 있어야 한다.
      ```

- 논리 언어

  - 기호 논리의 원리를 기반

  - 개체에 대한 사실과 개체 사이의 관계 규칙을 이용해 원하는 결과를 얻어낸다.

  - Prolog

    - ```
      father(a, c).
      male(X) :- father(X, Y).
      // male(a). -> 질의어
      ```

- 객체지향 언어

  - 명령형 언어, 함수 언어, 논리 언어 어느 것과도 결합이 가능하다.

  -  C++과 같이 명령형 언어를 확장한 객체지향 언어가 일반적

  - 객체(Object) 단위로 모든 처리를 기술

  - 객체는 데이터들과 연관된 동작들이 하나로 묶인 개념

  - 객체지향 언어는 추상 데이터 타입, 상속, 동적 바인딩 개념을 지원

  - C++

    - ```c++
      class Employee {
          private:
          char *name;
          public:
          Employee(char *na) {
              name = new char [strlen(na) + 1];
              strcpy(name, na);
          }
          ~Employee() {
              delete []name;
          }
          char* getName() {
              return name;
          }
      };
      Employee emp("abc");
      ```

    - emp의 구조

      -  ![클래스 예시](../../assets/Programming_Languages/8.PNG)
