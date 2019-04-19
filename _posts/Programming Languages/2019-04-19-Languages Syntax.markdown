---
layout: post
title:  "Languages Syntax"
description: "Languages Syntax"
date:   2019-04-19 19:08:00
categories: Programming_Languages
comments: true
---
- 언어 정의 - 구문과 의미로 구성되어 있다.

  - 자연어 정의, 형식 정의
  - 구문 형식 정의 - BNF, EBNF, 구문 조표

- 컴퓨터 - 프로그램을 실행할 수 있는 알고리즘 + 자료구조 집합

  - 하드웨어 컴퓨터(실제 컴퓨터), 소프트웨어 시뮬레이터 컴퓨터, 가상 컴퓨터(Virtual Computer)

- 가상 컴퓨터 : 고급언어 프로그래머는 컴퓨터를 가상의 고급 언어 컴퓨터로 간주

  - ![가상 컴퓨터](../../assets/Programming_Languages/10.PNG)

- 프로그래밍 언어의 기본 문자 집합

  - 알파벳 문자(A~Z) 26개 + 아라비아 숫자(0~9) 10개
  - ex) FORTRAN : 기본 문자 집합 + 13개의 특수 문자(+ - * / ( ) , . $ ' : 공백)
  - ex) ALGOL 60 : 알파벳 대소문자 52개 + 아라비아 숫자 10개 + 28개의 특수문자
    - ![ALGOL의 특수문자](../../assets/Programming_Languages/11.PNG)

- 문자 코드 체계

  - EBCDIC (Extended Binary Coded Decimal Interchange Code) : IBM에서 제안, 8비트 조합 코드
  - ASCII (American Standard Code for Information Interchange)
    - ANSI에서 제안, 7비트 조합 코드(128개의 문자 표현)
    - 영문자 대소문자 52개 + 숫자 10개 + 33개의 특수문자 + 33개의 제어문자
  - 유니코드 (Unicode) : 16bit, ISO 표준 규격, Java에 시행

- 정합 순서 (Collating Sequence) : 언어에 제공된 문자 순서

  - 일반적인 문자의 순서는 지킨다.
  - 구현 시 결정되는 코드 체계를 따른다. (프로그래머가 정의 가능 : RPG, SNOBOL)

- 어휘 구조 용어

  - 어휘 토큰(Lexical Token), 어휘 요소(Lexical Element), 어휘 단위(Lexical Unit)
  - 언어 구성자
  - 식별자(Identifier), 미리 정의된 식별자(Predefined Identifier), 예약어
  - 구분자, 분리자

- 예약어 (Reserved Words / Keywords)

  - 언어 어휘를 구선하는 단어나 기호 형태의 문자 알파벳
  - 프로그램의 변수 이름으로 사용할 수 없다.
  - 장점 : 프로그램 판독성 증가, 컴파일러가 기호 테이블을 빠른 시간에 탐색
  - 단점 : 많은 예약어를 기억하기 어려움, 언어 확장 시 새로운 예약어가 확장 이전에 사용했던 프로그램의 식별자와 중복 우려가 있다.

- BNF(Backus-Naur Form) 표기법

  - 구문(Syntax) 형식을 정의하는 가장 보편적인 표기법
  - 한 언어의 구문에 대한 BNF 정의 : 언어의 문장을 생성하는 생성 규칙(Production Rule) 정의
  - 생성 규칙 : 생성 규칙의 왼쪽(정의될 대상), 오른쪽에는 그 대상에 대한 정의가 표현
  - BNF 표기법에 의한 식별자(Identifier) 정의
  - ![BNF 표기 예시 & 메타 기호](../../assets/Programming_Languages/12.PNG)

- 문맥 자유 문법

  - Chomsky는 자연 언어에 대해 4가지 언어 유형의 문법을 제안
  - 프로그래밍 언어의 구문을 기술하는데 유용한 것으로 판명
  - 일련의 생성 규칙들로 구성되는 형식 (V -> w)

- Backus-Naur 형식

  - 배커스는 문맥 자유 문법과 유사한 형식의 표기법에 의해 구문이 기술된 ALGOL 58에 대한 논문을 발표
  - 1년 후 배커스의 표기법을 수정하여 ALGOL 60을 기술
  - 프로그래밍 언어의 구문을 기술하는데 매우 자연스러운 표기법

- BNF는 생성 규칙들의 집합 : 배정문에 대한 생성 규칙

  - ```
    <assign> -> <id> = <expr> . <assign> : 정의 되고 있는 구문 구조의 이름 - LHS(Left-Hand Side)
    ```

  - ```<id> = <expr> : LHS의 정의, RHS(Right-Hand Side)
    <id> = <expr> : LHS의 정의, RHS(Right-Hand Side)
    ```

  - ex) A = B + 10

    - ```
      'A'는 <id>에, 'B + 10'은 <expr>에 해당
      ```

  - 하나의 구문 구조는 두 개 이상의 다른 정의를 가질 수 있음.

    - ![구문 구조 예시](../../assets/Programming_Languages/13.PNG)

- 수에 대한 문법

  - ![수에 대한 문법](../../assets/Programming_Languages/14.PNG)

  - ```
    비단말 기호 : <number>, <digit>와 같이 '<>'로 묶인 기호, 다시 정의될 대상이라는 의미
    ```

  - 단말 기호 : 0, 1, 2와 같이 프로그램에 직접 나타낼 수 있는 기호, 각 괄호로 묶이지 않으며 알파벳, 숫자 문자 집합, 예약어

  - 메타 기호 : ->, < >, |와 같이 BNF 표기를 위하여 사용되는 특수 기호

- 유도

  - 문장 생성 과정
    - ![문장 생성 과정](../../assets/Programming_Languages/15.PNG)
    - ![문장 유도 과정](../../assets/Programming_Languages/16.PNG)

- 간단한 배정문에 대한 문법 (덧셈, 뺄셈 연산자와 괄호를 가진 산술식)

  - ![산술식 유도 과정](../../assets/Programming_Languages/17.PNG)

- 유도 : A = 3 + (5 - 2)

  - ![유도 예제](../../assets/Programming_Languages/18.PNG)
  - 문법 규칙에 의해 유도되지 않는 문장은 문법에 맞지 않는 것이라고 할 수 있다.
    - AB = 5 + (A * 3)

- 파스 트리

  - 유도 과정을 이해하기 쉬운 트리 형태의 계층적 구조로 나타낸 것
  - 파스 트리의 시작 기호는 루트
  - 123을 유도하는 파스 트리
    - ![123 유도 파스 트리](../../assets/Programming_Languages/19.PNG)
  - 파스 트리를 통한 유도에는 좌측 우선 유도와 우측 유선 유도가 있다.
  - A = 3 + 5 * 2
    - 이 식은 서로 다른 파스 트리가 두 개 나올 수 있다.
    - => 모호하다(Ambiguous) : 같은 문장에 대해 두 개 이상의 서로 다른 파스 트리가 생성되는 문법
    - ![모호한 유도](../../assets/Programming_Languages/20.PNG)
    - ![모호한 유도](../../assets/Programming_Languages/21.PNG)
    - 이 때에는 연산자 우선순위를 반영하여 유도 순서를 정해야 한다. (문법 개정이 필요하다.)
    - ![문법 개정 후 유도](../../assets/Programming_Languages/22.PNG)
    - ![문법 개정 후 유도](../../assets/Programming_Languages/23.PNG)
    - A = 3 - 5 - 2 : 좌측 우선 유도와 우측 우선 유도에 따라서도 서로 다른 파스 트리가 나올 수 있기 때문에 이 문법또한 모호하다.
    - ![문제점 발생](../../assets/Programming_Languages/24.PNG)
    - 문제가 발생하는 이유
      - ![문제 발생 이유](../../assets/Programming_Languages/25.PNG)
    - 모호하지 않은 문법
      - ![모호하지 않은 문법](../../assets/Programming_Languages/26.PNG)
      - ![모호하지 않은 파스 트리](../../assets/Programming_Languages/27.PNG)

- EBNF

  - BNF가 지닌 몇 가지 사소한 불편을 개선한 표기법
  - BNF 표기법을 확장하여 보다 읽기 쉽고, 간단하게 표현된 표기법
  - 반복을 의미하는 { }, 옵션을 의미하는 [ ], 다중 선택을 의미하는 ( )
  - ![반복](../../assets/Programming_Languages/28.PNG)
  - ![옵션](../../assets/Programming_Languages/29.PNG)
  - ![다중 선택](../../assets/Programming_Languages/30.PNG)
