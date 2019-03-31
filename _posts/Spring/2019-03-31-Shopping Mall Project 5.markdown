---
layout: post
title:  "Shopping Mall Project 5 - Signup, Signin, Signout"
description: "Shopping Mall Project 5 - Signup, Signin, Signout"
date:   2019-03-31 19:05:00
categories: Spring
comments: true
---
- 라이브러리 추가 (pom.xml)
```
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.hyun</groupId>
  <artifactId>shopping_mall_example</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>shopping_mall_example Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.1.5.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-web -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.1.5.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.1.5.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-core -->
    <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-core</artifactId>
      <version>5.1.4.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-web -->
    <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-web</artifactId>
      <version>5.1.4.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-config -->
    <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-config</artifactId>
      <version>5.1.4.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.1.5.RELEASE</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.15</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.0</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>2.0.0</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.8</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
    <dependency>
      <groupId>org.projectlombok</groupId>
      <artifactId>lombok</artifactId>
      <version>1.18.6</version>
      <scope>provided</scope>
    </dependency>

    <!-- https://mvnrepository.com/artifact/javax.servlet/jstl -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-api -->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>1.8.0-beta4</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>5.1.5.RELEASE</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <finalName>shopping_mall_example</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

- 웹 페이지의 공통 부분 작성 (WEB-INF/views/include)
  - header.jsp
    ```
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <h1 class="title">
        <a href="/">Hyun</a>
    </h1>
    ```

  - nav.jsp
    ```
    <%@ page contentType="text/html;charset=UTF-8" language="java" pageEncoding="UTF-8" %>
    <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

    <ul>
        <c:if test="${user == null}">
            <li>
                <a href="/user/signin">로그인</a>
            </li>
            <li>
                <a href="/user/signup">회원가입</a>
            </li>
        </c:if>
        <c:if test="${user != null}">
            <c:if test="${user.isEmailVerified == 9}">
                <a href="/admin/index">관리자 화면</a>
            </c:if>
            <li>
                ${user.username} 님, 환영합니다!
            </li>
            <li>
                <a href="/user/signout">로그아웃</a>
            </li>
        </c:if>
    </ul>
    ```

  - footer.jsp
    ```
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <ul>
        <li>사이트 소개</li>
        <li>이용약관</li>
        <li>hyun</li>
    </ul>
    ```

## 1. Signup, Signin, Signout

### (1) mapper 추가 (userMapper.xml)
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.hyun.shopping_mall_example.mapper.userMapper">

    <!-- 회원 가입 -->
    <insert id="signup">
        insert into user(name, username, password, phone_number, address, detail_address, zipcode) values (#{name}, #{username}, #{password}, #{phoneNumber}, #{address}, #{detailAddress}, #{zipcode})
    </insert>

    <!-- 로그인 -->
    <select id="signin" resultType="com.hyun.shopping_mall_example.domain.UserVO">
        select * from user
        where username = #{username}
    </select>

</mapper>
```

### (2) DAO, Service, Controller 추가
- UserDAO
  ```
  @Repository
  public class UserDAO {
      private SqlSession sqlSession;

      private static final String mapper = "com.hyun.shopping_mall_example.mapper.userMapper";

      public UserDAO(SqlSession sqlSession) {
          this.sqlSession = sqlSession;
      }

      public void signup(UserVO userVO) throws Exception {
          sqlSession.insert(mapper + ".signup", userVO);
      }

      public UserVO signin(UserVO userVO) throws Exception {
          return sqlSession.selectOne(mapper + ".signin", userVO);
      }
  }
  ```

- UserService (Interface)
  ```
  public interface UserService {
      public void signup(UserVO userVO) throws Exception;
      public UserVO signin(UserVO userVO) throws Exception;
  }
  ```
- UserServiceImpl
  ```
  @Service
  public class UserServiceImpl implements UserService {
      private UserDAO userDAO;
      private BCryptPasswordEncoder bCryptPasswordEncoder;

      public UserServiceImpl(UserDAO userDAO, BCryptPasswordEncoder bCryptPasswordEncoder) {
          this.userDAO = userDAO;
          this.bCryptPasswordEncoder = bCryptPasswordEncoder;
      }

      @Override
      public void signup(UserVO userVO) throws Exception {
          userVO.setPassword(bCryptPasswordEncoder.encode(userVO.getPassword()));
          userDAO.signup(userVO);
      }

      @Override
      public UserVO signin(UserVO userVO) throws Exception {
          UserVO loginUser = userDAO.signin(userVO);
          if (loginUser == null) return null;
          boolean matchPassword = bCryptPasswordEncoder.matches(userVO.getPassword(), loginUser.getPassword());
          if (!matchPassword) return null;
          return loginUser;
      }
  }
  ```

- UserController
  ```
  @Controller
  @RequestMapping("/user")
  public class UserController {
      private static final Logger Logger = LoggerFactory.getLogger(UserController.class);

      private UserService userService;

      public UserController(UserService userService) {
          this.userService = userService;
      }

      @GetMapping(value = "/signup")
      public void signup() throws Exception {
          Logger.info("Get Signup");
      }

      @PostMapping(value = "/signup")
      public String signup(UserVO userVO) throws Exception {
          Logger.info("Post Signup");
          userService.signup(userVO);
          return "redirect:/";
      }

      @GetMapping(value = "/signin")
      public void signin() throws Exception {
          Logger.info("Get Signin");
      }

      @PostMapping(value = "/signin")
      public String signin(UserVO userVO, HttpServletRequest httpServletRequest, RedirectAttributes redirectAttributes) throws Exception {
          UserVO loginUser = userService.signin(userVO);
          HttpSession httpSession = httpServletRequest.getSession();
          if (loginUser == null) {
              httpSession.setAttribute("user", null);
              redirectAttributes.addFlashAttribute("msg", false);
              return "redirect:/user/signin";
          }
          httpSession.setAttribute("user", loginUser);
          return "redirect:/";
      }

      @GetMapping(value = "/signout")
      public String signout(HttpSession httpSession) throws Exception {
          Logger.info("Get Signout");
          httpSession.invalidate();
          return "redirect:/";
      }
  }
  ```
### (3) 로그인, 회원가입 페이지 작성 (WEB-INF/views/user)
- signup.jsp
  ```
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
      <head>
          <title>Hyun</title>
      </head>
      <body>
          <div id="root">
              <header id="header">
                  <div id="header_box">
                      <%@ include file="../include/header.jsp"%>
                  </div>
              </header>
              <nav id="nav_box">
                  <%@ include file="../include/nav.jsp"%>
              </nav>
              <section id="container">
                  <div id="container_box">
                      <section id="content">
                          <form role="form" method="post" autocomplete="off">
                              <div class="input_area">
                                  <label for="username">Username : </label>
                                  <input type="email" id="username" name="username" placeholder="example@email.com" required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="password">Password : </label>
                                  <input type="password" id="password" name="password" required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="name">Name : </label>
                                  <input type="name" id="name" name="name" placeholder="이름을 입력해주세요." required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="phoneNumber">Phone_number : </label>
                                  <input type="phoneNumber" id="phoneNumber" name="phoneNumber" placeholder="'-'를 제외한 연락처를 입력해주세요." required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="address">주소 : </label>
                                  <input type="address" id="address" name="address" placeholder="주소를 입력해주세요." required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="detailAddress">상세 주소 : </label>
                                  <input type="detailAddress" id="detailAddress" name="detailAddress" placeholder="상세 주소를 입력해주세요." required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="zipcode">우편번호 : </label>
                                  <input type="zipcode" id="zipcode" name="zipcode" placeholder="우편번호를 입력해주세요." required="required" />
                              </div>
                              <button type="submit" id="signup_btn" name="signup_btn">회원가입</button>
                          </form>
                      </section>
                  </div>
              </section>
              <footer id="footer">
                  <div id="footer_box">
                      <%@ include file="../include/footer.jsp" %>
                  </div>
              </footer>
          </div>
      </body>
  </html>
  ```

- signin.jsp
  ```
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
      <head>
          <title>Hyun</title>
      </head>
      <body>
          <div id="root">
              <header id="header">
                  <div id="header_box">
                      <%@ include file="../include/header.jsp"%>
                  </div>
              </header>
              <nav id="nav_box">
                  <%@ include file="../include/nav.jsp"%>
              </nav>
              <section id="container">
                  <div id="container_box">
                      <section id="content">
                          <form role="form" method="post" autocomplete="off">
                              <div class="input_area">
                                  <label for="username">Username : </label>
                                  <input type="email" id="username" name="username" placeholder="example@email.com" required="required" />
                              </div>
                              <div class="input_area">
                                  <label for="password">Password : </label>
                                  <input type="password" id="password" name="password" required="required" />
                              </div>
                              <button type="submit" id="signin_btn" name="signin_btn">로그인</button>
                              <c:if test="${msg == false}">
                                  <p style="color: #ff000000;">Login Failed</p>
                              </c:if>
                          </form>
                      </section>
                  </div>
              </section>
              <footer id="footer">
                  <div id="footer_box">
                      <%@ include file="../include/footer.jsp" %>
                  </div>
              </footer>
          </div>
      </body>
  </html>
  ```