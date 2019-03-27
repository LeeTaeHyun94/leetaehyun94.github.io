---
layout: post
title:  "Shopping Mall Project 2 - SQL Connection Setting"
description: "Shopping Mall Project 2 - SQL Connection Setting"
date:   2019-03-27 23:40:00
categories: Spring
comments: true
---
## 1. MySQL 설치 및 실행 확인
Ubuntu 18.04에 MySQL 5.7.25 설치.
내가 설치한 버전은 설치 도중에 root 패스워드를 설정하지 않기 때문에 아래와 같이 진행하자.

(1) sudo mysql_secure_installation

(2) VALIDATE PASSWORD plugin 설정 여부 : y

(3) 패스워드 강도 설정 : 1

(4) root 패스워드 입력, 재입력

(5) 데이터베이스를 아무나 읽어볼 수 없게 설정할 것인지 여부 : y

(6) 원격 접속으로 root 계정 사용할 수 없게 할 것인지 여부 : y

(7) 테스트 데이터베이스 삭제 여부 : y

(8) 권한 설정 테이블 reload : y

root 계정을 사용해도 괜찮지만, 나는 직접 계정을 생성하고 root 계정을 통해 schema를 생성한 뒤, 직접 생성한 계정에 접근 권한을 주었다.
```
$ sudo mysql
mysql> create schema test DEFAULT CHARACTER SET utf8;
mysql> create user {username} identified by 'password';
mysql> grant all privileges on test.* to 'username'@'localhost' identified by 'password';
```

위의 설정 과정을 거친 후 mysql -u {username} -p > 패스워드 입력 과정을 통해 MySQL을 이용해주면 된다.

## 2. JDBC, MyBatis Setting in Spring

(1) pom.xml에 의존성 추가 (spring-jdbc, mysql-connector-java, mybatis, mybatis-spring)

(2) resources 디렉토리에 mybatis-config.xml, mapper 추가

(3) applicationContext에서 bean 설정

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
		<bean class="org.springframework.jdbc.datasource.DriverManagerDataSource" id="dataSource">
			<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
			<property name="url" value="jdbc:mysql://localhost:3306/test?serverTimezone=UTC&amp;useUnicode=True&amp;characterEncoding=utf-8"/>
			<property name="username" value="username"/>
			<property name="password" value="password"/>
		</bean>

		<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
			<property name="dataSource" ref="dataSource"/>
			<property name="configLocation" value="classpath:/mybatis/mybatis-config.xml"/>
			<property name="mapperLocations" value="classpath:mapper/**/*Mapper.xml"/>
		</bean>

		<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate" destroy-method="clearCache">
			<constructor-arg name="sqlSessionFactory" ref="sqlSessionFactory"/>
		</bean>
	</beans>

(4) Test Code 작성

	package controller;

	import org.apache.ibatis.session.SqlSession;
	import org.apache.ibatis.session.SqlSessionFactory;
	import org.junit.Test;
	import org.junit.runner.RunWith;
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.test.context.ContextConfiguration;
	import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

	import javax.sql.DataSource;
	import java.sql.Connection;

	@RunWith(SpringJUnit4ClassRunner.class)
	@ContextConfiguration(locations = {"classpath:spring/applicationContext.xml"})
	public class SqlConnectionTest {
		@Autowired
		private DataSource dataSource;

		@Autowired
		private SqlSessionFactory sqlSessionFactory;

		@Test
		public void test() throws Exception {
			try (Connection connection = dataSource.getConnection()) {
				System.out.println(connection);
			}
			catch (Exception e) {
				e.printStackTrace();
			}
		}

		@Test
		public void factoryTest() {
			System.out.println(sqlSessionFactory);
		}

		@Test
		public void sessionTest() throws Exception {
			try (SqlSession sqlSession = sqlSessionFactory.openSession()) {
				System.out.println(sqlSession);
			}
			catch (Exception e) {
				e.printStackTrace();
			}
		}
	}

- JUnit Test가 무사히 통과하면 SQL Connection 설정이 완료된 것.
