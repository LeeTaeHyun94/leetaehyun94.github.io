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
- Maven + Spring MVC

  (1) Maven 선택 > Create from archetype 체크 > org.apache.maven.archetypes:maven-archetype-webapp 선택하고 Next

  (2) GroupId, ArtifactId 채워넣고 Next 누르다가 Finish

  (3) pom.xml 파일에 의존성 추가 (spring-web, spring-webmvc)
  
  (4) Spring 설정 파일 (src/main/resources/spring/applicationContext.xml, src/main/resources/spring/appServlet/dispatcher-servlet.xml) 추가, Mark Directory As Resources Root
	- dispatcher-servlet.xml
		```
		<?xml version="1.0" encoding="UTF-8"?>
		<beans xmlns="http://www.springframework.org/schema/beans"
			xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			xmlns:mvc="http://www.springframework.org/schema/mvc"
			xmlns:context="http://www.springframework.org/schema/context"
			xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
			http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
			http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
			<mvc:annotation-driven/>
			<context:component-scan base-package="com.hyun.shopping_mall_example"/>

			<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
				<property name="prefix" value="/"/>
				<property name="suffix" value=".jsp"/>
			</bean>
		</beans>
		```

  (5) Source Directory (ex : src/main/java/{groupId}/{ArtifactId}) 추가, Mark Directory As Source Root

  (6) web.xml 설정
	```
	<!DOCTYPE web-app PUBLIC
	"-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
	"http://java.sun.com/dtd/web-app_2_3.dtd" >

	<web-app>
	<display-name>Archetype Created Web Application</display-name>

	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath:spring/applicationContext.xml</param-value>
	</context-param>
	
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>

	<servlet>
		<servlet-name>dispatcher</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath:spring/appServlet/dispatcher-servlet.xml</param-value>
		</init-param>
	</servlet>
	
	<servlet-mapping>
		<servlet-name>dispatcher</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
	</web-app>
	```

- Run Configuration 설정

  (1) `+` 버튼을 누르고 Tomcat Server > Local 선택하고 이름을 설정

  (2) Server 탭의 Application server: `Configure...` 버튼을 클릭하고 Tomcat 설치한 디렉토리로 설정

  (3) Deployment 탭에서 Artifact 추가
	- 이 때 Application context로 아무것도 설정하지 않으면(/) end-point에 프로젝트 이름이 추가되지 않는다.

여기까지 하면 Intellij에서 만든 Spring MVC Project가 Tomcat에서 실행이 되는 것을 확인할 수 있다.
