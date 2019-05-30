---
layout: post
title: "Spring Framework"
description: "Spring Framework"
date: 2019-05-30 19:05:00
categories: Spring
comments: true
---

## 1. 정의
- 자바 플랫폼을 위한 오픈 소스 어플리케이션 프레임워크
- 자바 엔터프라이즈 개발을 편하게 해주는 오픈 소스 경량급 어플리케이션 프레임워크
- 자바 개발을 위한 프레임워크로 종속 객체를 생성해주고, 조립해주는 도구
- POJO(Plain Old Java Object) Bean Container  
위처럼 스프링 프레임워크에 대한 다양한 정의가 있지만, 위의 정의들만으로는 정확한 이해가 어렵기 때문에 나름의 핵심적인 정의를 내리자면,  
### 스프링 프레임워크는 DI(Dependency Injection)와 IoC(Inversion of Control)를 제공하는 하나의 컨테이너라고 생각한다.  
![Spring Triangle](../../assets/Spring/1.PNG)

## 2. 특징
위의 정의를 이해하기 위해 스프링 프레임워크의 특징을 서술하자면,
- POJO (Plain Old Java Object) : Java EE를 사용하면서, 해당 플랫폼에 종속되어 있는 무거운 객체들을 만드는 것에 부정적인 의견을 제시하며 나타난 용어로서, 별도의 프레임워크 없이 Java EE를 사용할 때에 비해 POJO 방식은 특정 인터페이스를 직접 구현하거나 상속받을 필요가 없어 기존 라이브러리를 지원하기가 용이하고, 객체가 가볍다는 장점이 있다.
- AOP (Aspent Oriented Programming) : 로깅, 트랜잭션, 보안 등 여러 모듈에서 공통적으로 사용하는 기능을 분리하여 관리할 수 있다.
- DI (Dependency Injection) : 구성 요소 간의 의존 관계가 소스 코드 내부가 아닌 외부의 설정 파일을 통해 정의되는 방식, 코드의 재사용성을 높여 소스 코드를 다양한 곳에 재사용 가능하며, 모듈 간의 결합도도 낮출 수 있다.
- IoC (Inversion of Control) : 이전의 프로그래밍에서는 개발자가 작성한 프로그램이 외부 라이브러리의 코드를 호출해서 이용했지만, 제어 역전은 이와 반대로 외부 라이브러리 코드가 개발자의 코드를 호출하게 된다. 한마디로, 제어권이 프레임워크에 있다는 것.
- PSA (Portable Service Abstraction) : 스프링 프레임워크는 다른 여러 가지 모듈을 사용함에 있어 별도의 추상화 레이어를 제공한다.
- 스프링 프레임워크는 Java Bean(객체)의 생성, 소멸을 직접 관리하며, 필요한 객체만 사용할 수 있다.

다시 스프링을 설명한다면, 1) 사용자는 필요한 객체들을 보다 간단하게 정의하고, 2) 모듈 간의 의존성은 소스 코드가 아닌 설정 파일에서 정의하여 스프링 프레임워크가 연결시키도록 하여 코드의 재사용성을 높이고, 3) 어플리케이션에 필요한 라이브러리들은 프로젝트 관리 도구를 통해 손쉽게 추가, 제거함으로써 필요한 라이브러리만 사용하고 사용된 라이브러리 코드를 기반으로 스프링 프레임워크에서 사용자가 작성한 코드를 호출하여 사용하게 된다. 이외에도 더 많은 역할을 수행하지만,  
#### 스프링 프레임워크의 핵심은 크게 위의 세 가지 역할을 수행하는 하나의 컨테이너라고 볼 수 있다.

## 3. 구조
![Structure of Spring Framework](../../assets/Spring/2.PNG)  
스프링 프레임워크는 약 20 개의 모듈로 구조화되어 있다.

### (1) Core Container
- Core, Beans
  - IoC와 DI를 포함하여 프레임워크의 기본이 되는 기능을 제공한다.
  - BeanFactory는 팩토리 메서드 패턴을 이용하여 구현되어 있고, 이를 통해 Java Bean에 대한 싱글턴 패턴 구현이나, 실제 프로그램 로직에서 의존성에 대한 설정과 명세를 분리할 수 있다.
- Context : Beans 모듈의 특징을 상속받고 전역화, 이벤트 전달, 리소스 적재, Servlet Container Context의 투명한 생성에 대한 기능들을 지원한다.
- Expression Language : 런타임 시 객체를 조회하고 조작하는 표현 언어
  - Property Getter/Setter, 속성 할당, 메서드 호출, 배열, 컬렉션과 인덱서의 컨텍스트 접근, 논리적/산술적 연산자, 이름 있는 변수, 스프링의 IoC 컨테이너에서 이름으로 객체를 획득하는 기능 등을 지원한다.

### (2) Data Access/Integration
- JDBC : JDBC 추상화 계층을 제공
- ORM : JPA, JDO, Hibernate, iBatis 등 객체-관계 매핑 API에 대해 통합된 추상화 계층을 제공한다. (ORM 라이브러리를 통해 트랜잭션 관리 등 스프링의 다른 기능들과 함께 사용할 수 있다.)
- OXM : JAXB, Castor, XMLBeans, JiBX, XStream 등 객체-XML 매핑 구현을 지원한다.
- JMS (Java Messaging Service) : 메시지를 생산하고 소비하는 기능 (여기서 말하는 메시지는 어플리케이션 간 데이터를 주고 받기 위한 수단이라고 생각)
- Transactions : 특별한 인터페이스와 모든 POJO 클래스에 대한 트랜잭션 관리를 지원한다. (소스 코드나 어노테이션 선언으로 가능하다.)

### (3) Web
- Web : 기본적인 웹 지향적인 통합 기능(Mutipart File Upload, Servlet Listener, 웹 지향적인 어플리케이션 컨텍스트를 사용한 IoC 컨테이너의 초기화 등)
- Web-Servlet : 웹 어플리케이션을 위한 스프링의 MVC 구현을 포함한다.
  - 스프링의 MVC 프레임워크는 도메인 모델 코드와 웸 폼을 깔끔하게 분리할 수 있도록 하고 스프링의 다른 모든 기능과 통합 가능하다.
- Web-Struts : 이전의 스트러츠 웹 티어를 통합하는 클래스를 포함, 스프링 3.0에서 폐기
- Web-Portlet : 포틀릿 환경에서 사용되는 MVC 구현과 Web-Servlet 모듈 기능의 미러 버젼을 제공한다.

### (4) AOP, Aspects Instrumentation
- AOP : AOP Alliance를 따르는 관점 지향 프로그래밍의 구현체
  - 예를 들어, 기능적으로 분리되어야 하는 코드에 대해 Method Interceptor, PointCut 등을 정의할 수 있다.
- Aspects : AspectJ와의 통합을 제공한다.
- Instrumentation : Instrumentation을 지원하는 클래스와 특정 어플리케이션 서버에서 사용되는 Class Loader 구현체를 제공한다.

### (5) Test
JUnit이나 TestNG로 스프링 컴포넌트에 대한 테스트를 지원한다. 테스트 모듈 또한 전체 어플리케이션 모듈과 마찬가지로 스프링 어플리케이션 컨텍스트의 로딩과 캐싱을 제공한다. 또한, 코드를 격리되상태로 테스트하기 위해 사용할 수 있는 모의 객체를 제공한다.
