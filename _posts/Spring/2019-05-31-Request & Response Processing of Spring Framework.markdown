---
layout: post
title: "Request & Response Processing of Spring Framework"
description: "Request & Response Processing of Spring Framework"
date: 2019-05-31 18:00:00
categories: Spring
comments: true
---
Spring MVC Project의 관점에서 서버에 요청이 올 경우의 과정

### Web Page 요청 시
![Spring MVC Structure (Default)](../../assets/Spring/3.PNG)

### RESTful API 요청 시
![Spring MVC Structure (RESTful)](../../assets/Spring/4.PNG)

## 1. 과정  
(1) 클라이언트가 서버에 요청을 보내면, 스프링에서 제공하는 DispatcherServlet 클래스에서 요청을 가로챈다.  
- Spring MVC Project는 First Controller 패턴을 사용하고 있다.
  - First Controller : 어플리케이션의 가장 앞 쪽에 모든 요청을 받는 서블릿을 두고 들어오는 요청에 대해 개발자가 명시한 것에 따라 직접 분기하여 요청을 처리하는 방식
- 위에서 서술한 First Controller의 역할을 DispatcherServlet 클래스가 수행한다.
- web.xml 파일을 통해 URL과 서블릿을 매핑하여 DispatcherServlet이 모든 요청을 가로챌 수 있다.
- DispatcherServlet 앞에는 Filter라는 것이 있어 HTTP Request Header 등 요청에 담긴 정보를 읽어들여 DispatcherServlet에 진입하기 전 필요한 사전처리를 수행한다.
- DispatcherServlet은 한 개일 수도 있고 여러 개일 수도 있다. 위에 서술한대로 한 개의 DispatcherServlet으로 모든 요청을 받고 IoC Container에 진입해서 분기처리할 수 있기 떄문에 Legacy JSP와 호환을 위한 경우가 아니면 여러 개의 DispatcherServlet으로 운용할 필요는 없다.  

(2) DispatcherServlet에서 URL에 적합한 컨트롤러를 매핑시킨다.
- 이 과정에서 우리는 일반적으로 어노테이션(@RequestMapping, @GetMapping, @PostMapping ...)을 이용해 요청 방식에 대한 매핑을 하기 떄문에 AnnotationMethodHandlerAdapter가 사용된다.
- AnnotationMethodHandlerAdapter에서는 @Controller, @RestController로 어노테이션 정의되어 있는 컨트롤러 클래스를 스캔하여 URL과 요청 방식에 맞는 메소드를 찾는다.
- HandlerAdapter는 handle() 메서드 하나만 존재하는 간단한 인터페이스인데, 적합한 컨트롤러를 찾아 HttpServletRequest를 전달하고 모든 로직을 마친 후, 응답을 반환하는 역할을 수행한다.

(3) 요청에 매핑된 컨트롤러에서는 해당 요청을 처리하기 위해 Service를 주입(DI)받아 비즈니스 로직을 Service 클래스로 위임한다.  

(4) Service에서는 요청에 필요한 작업 대부분을 처리하며 데이터베이스에 접근이 필요한 경우에는 DAO를 주입받아 데이터베이스 처리 로직을 DAO 클래스로 위임한다.  

(5) DAO(Data Access Object)는 mybatis나 hibernate 등 Persistence Framework를 사용하여 데이터베이스 처리를 위한 작업(SQL or NoSQL 등 DBMS에 따른 쿼리 수행)을 수행한다.
- 이 때, 보통 필요한 데이터 혹은 반환해야 할 데이터는 VO(Value Object)를 그대로 사용하거나 별도로 정의한 DTO(Data Transfer Object)를 사용하여 Controller, Service, DAO 각 레이어를 거쳐 전달(Controller -> Service -> DAO or DAO -> Service -> Controller)한다.
- Persistence Framework : 영속성(Persistence)은 어플리케이션이 종료되더라도 데이터는 사라지지 않는 특성을 의미하며, Persistence Framework는 결국 데이터의 영속성을 유지하기 위한 데이터베이스를 조작하는 프레임워크라고 할 수 있다.
  - 데이터베이스를 조작하기 위해서는 JDBC를 이용하여 프로그래밍해야 하는데, JDBC 프로그래밍의 반복 작업이나 복잡한 작업에 대해 라이브러리화하여 편의성을 제공한다.
  - SQL Mapper와 ORM으로 나눌 수 있다.
  - SQL Mapper : 직접 SQL 쿼리를 작성해 데이터베이스를 조작한다. 대표적으로 Mybatis가 있다.
    - 단순히, 직접적으로 필드를 매핑시키는 것을 지향
  - ORM (Object Relational Mapping) : 객체와 데이터베이스 스키마를 매핑하여 간접적으로 데이터베이스를 조작한다.
    - 데이터베이스 스키마를 객체로 매핑하고, 스키마 간의 관계를 객체에 별도로 정의한다.
    - 관계형 DBMS가 아니어도 사용할 수 있다.
    - SQL 쿼리를 정의하지 않아도 객체에 스키마 간의 관계가 설계한대로 잘 정의되어 있다면, 메서드만으로 데이터베이스를 조작 가능하다. (내부적으로 DBMS에 따라 수행할 쿼리문을 관계에 맞게 자동 생성하여 수행한다.)  

(6) 모든 로직을 끝내고 각 계층에 해당하는 결과를 반환하며, 컨트롤러로 돌아오게 된다.

(7) 컨트롤러에서는 두 가지 경우에 따라 ModelAndView 객체을 반환하거나, 요청한 데이터에 대한 객체를 DispatcherServlet으로 반환한다.
- @ResponseBody, @RestController의 경우
  - 일반적으로, ResponseEntity 객체를 활용하여 요청한 데이터에 대한 객체와 HTTP Status Code(요청 처리 상태에 대해 알 수 있다.)를 함께 반환한다.
- 그 외의 경우
  - ModelAndView 객체를 활용하여 view로 사용할 JSP 파일의 경로와 view에서 사용될 데이터를 하나로 묶어 반환할 수 있다.
  - 또 다른 방법은 컨트롤러 메서드의 매개변수에 Model을 추가하여 view에서 사용될 데이터는 Model에 포함시키고 view로 사용할 JSP 파일의 경로를 문자열로 반환할 수 있다.  

(8) DispatcherServlet에서는 두 가지 경우에 따라 다르게 처리하고 응답(HTTP Response)을 반환한다.
- @ResponseBody, @RestController의 경우
  - MessageConverter 클래스를 이용하여 반환된 객체를 전략에 따라 적절한 메시지로 변환하여 직접 HTTP Response Body에 기록한다.
    - 대표적인 케이스로, Jackson2HttpMessageConverter를 이용하여 컨트롤러가 반환한 객체를 문자열로 변환하여 이 내용을 HTTP Response Body에 기록한다.
  - 기록된 응답을 반환한다.
- 그 외의 경우
  - ViewResolver 클래스를 이용하여 JSP 파일의 경로에 따라 해당 JSP 파일을 찾아 DispatcherServlet에 알려준다.
  - 그 다음, view에 대한 렌더링을 지시하고 응답을 돌려준다.  
