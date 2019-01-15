---
layout: post
title:  "RESTful API"
description: "RESTful API - Resource oriented architecture"
date:   2019-01-15 21:00:00
categories: Web
comments: true
---
## 1. Concept
REpresentational State Transfer
- 웹으로 접근할 수 있는 자원을 URI로 정의하고 해당 자원에 대한 조회, 갱신, 삭제, 삽입 메서드를 통해 이용할 수 있도록 하는 구조
- 자원 하나하나가 모두 식별자(URI)를 갖는다.

## 2. Structure
- HTTP Method (GET, POST, DELETE, PUT, ...)

### * HTTP Method with idempotent

- URI (Uniform Resource Identifier) : 리소스의 고유 식별자

## 3. Benefit
- 직관적인 표현 - 프론트엔드와 백엔드의 분리
    - View 영역이 포함되지 않은 서버 사이드 개발 진행
    - 플랫폼 종속적이지 않은 API 제공 가능

## 4. Feature
1. Uniform Interface : 플랫폼, 언어에 의존적이지 않다.
    - 단, json, xml과 같은 범용적인 Content Type을 사용
2. Stateless (무상태성) : 상태 값을 저장하지 않는다.
    - 세션과 같은 처리를 하지 않기 때문에 구현이 단순해진다.
3. Cacheable (캐싱 가능) : 네트워크 응답시간 뿐만 아니라, 자원 사용률을 비약적으로 향상시킬 수 있다.
4. Self-destructive (자체 표현구조) : 직관적인 표현으로, 최소한의 문서만으로 파악할 수 있다.
5. Client/Server structure (클라이언트/서버 구조) : 서버 사이드와 클라이언트 사이드가 명확하게 분리된다.
    - 계층형 구조 : 클라이언트 입장에서는 REST API 서버만 호출하지만 서버는 다중 계층으로 구성될 수 있다.
        - 순수 비즈니스 로직을 수행하는 API 서버와 그 앞단에 사용자 인증(Authentication), 암호화(SSL), Load Balancing 등을 하는 계층을 추가해서 구조 상의 유연성을 들 수 있다.
        - MSA(Micro Service Architecture)의 API Gateway, Reverse Proxy(HA Proxy, Apache 등)를 이용해서 구현한다.

## 5. Guide for design
1. 심플하고 직관적인 URI 구성
    - 리소스는 명사를 사용하여 표현
    - /로 계층 표현 가능
    - 파일 확장자는 포함하지 않는다.
2. 자원에 대한 행위(작업) 정의
    - 리소스에 대한 행위는 메서드로
    - GET, POST, DELETE, PUT으로 표현할 수 없는 동작은 URI와 문맥을 함께 구성
        - 다른 메서드들도 추가되어 있다.
3. Error Handling : 에러 처리의 기본은 HTTP Response code를 사용하고, Response body에는 에러에 대한 명세가 있어야 한다.
    - HTTP Response code
        - 200 Success - 성공
        - 400 Bad Request - field validation 실패
        - 401 Unauthorized - API 인증, 인가 실패
        - 404 Not Found - 해당 리소스가 없음
        - 500 Internal Server Error - 서버 에러
4. API 버전 관리
5. 페이징 : 파라미터로 x 번째 레코드부터 y 개를 나타내는 형태를 권장한다. (/record?offset=100&limit=25)
6. Partial Response 처리
    - 리소스에 대한 응답 메시지에 대해서 굳이 모든 필드를 포함할 필요가 없는 케이스에 사용
    - ex)
        - /people:(id,first-name,last-name,industry) // LinkedIn
        - /people?fields=id,name // Facebook
        - ?fields=title,media:group(media:thumbnail) // Google : JSON의 sub-object 개념
7. 검색 (전역검색과 지역검색)
    - 일반적으로 Query String에 검색 조건을 정의한다.
    - 만약 다른 성질의 Query String과 섞일 때는 =(등호)를 URLEncoding을 통해 다른 (%3D 등)Deleminator로 표현하여 하나의 Query String으로 만드는 것이 좋다.
    - 전역검색 시에는 전역검색만을 위한 URI를 설계하는 것이 좋다.
8. HATEOAS(Hypermedia As The Engine Of Application State)를 이용한 링크 처리
    - 하이퍼미디어의 특징을 이용하여 HTTP Response에 다음 Action 등 관계되는 리소스에 대한 HTTP link를 함께 리턴하는 것
9. 단일 API Endpoint 활용
    - API 서버가 물리적으로 분리된 여러 개의 서버에서 동작하고 있을 때, user.apiserver.com, car.apiserver.com과 같이 API 서비스마다 URL에 분리되어 있으면 개발자가 사용하기 불편하다.
    - 때문에 API 서비스는 물리적으로 서버가 분리되어 있더라도 HAProxy나 Nginx와 같은 Reverse Proxy를 사용하여 단일 URL을 사용하는 것이 좋다.
    - 이렇게 하면, 향후 API 서버들이 확장되더라도 API를 사용하는 클라이언트 입장에서는 단일 엔드포인트를 보게되고, 관리 면에서도 단일 엔드포인트를 통해서 부하 분산 및 로그를 통한 Audit(감사) 등을 할 수 있기 때문에 편리하다.
    - 서버의 유연한 운용 가능
8. Anti-pattern (피해야 하는 디자인)
    - GET/POST 메서드를 이용한 Tunneling
        - GET을 이용한 터널링 - http://myweb/users?method=update&id=terry : 실제 동작은 리소스를 업데이트하는 내용인데 PUT을 이용하지 않고 parameter로 수정 메서드임을 명시했다.
            - 이는 REST라고도 할 수 없고, 웹 캐시 인프라 등도 사용할 수 없다.
        - POST를 이용한 터널링 - Insert(Create)의 성질을 갖는 operation이 아님에도 불구하고 JSON body에 동작 내용과 필요한 정보를 넘겨 POST 메서드로 요청하는 형태
    - HTTP Response code를 사용하지 않음

## 6. Weak point
### (1) 단점
1. 메서드의 제약 - 존재하는 HTTP 메서드로 표현할 수 없는 작업들의 URI를 구성할 때, 복잡해질 수 있다.
2. RDBMS를 자원으로 할 때, 복잡도가 증가한다. (검색 필터가 증가할 수록 URI 구성이 힘듦.)
3. 표준 규약이 없기 때문에 시스템 설계자에 따라서 구성이 상이하다.
    - 비표준에서 오는 관리의 문제점은 제대로 된 REST API 표준 가이드와 API 개발 전후로 API Docs(Specification)를 제대로 만들어서 리뷰하는 프로세스를 갖추는 방법으로 해결해야 한다.
4. HTTP + JSON만 쓴다고 REST가 아니기 때문에 REST에 대한 제대로 된 이해가 수반되어야 한다.
### (2) 응용(개선) 방향
1. 자원 중심의 설계를 선행 - '무엇을 제공할 것인가?'를 정의하고, 그에 맞는 URI를 확립하는 작업에 많은 시간을 들인다.
2. 무상태성을 지향하는 구조 - '세션' 등 상태 정보를 기반으로 정보 접근 권한을 부여하는 시스템에는 부적합하다.
