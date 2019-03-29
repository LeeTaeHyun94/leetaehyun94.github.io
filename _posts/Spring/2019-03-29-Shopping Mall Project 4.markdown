---
layout: post
title:  "Shopping Mall Project 4 - Create Tables, Value Objects"
description: "Shopping Mall Project 4 - Create Tables, Value Objects"
date:   2019-03-29 12:00:00
categories: Spring
comments: true
---
## 1. Create Tables

### (1) User
- id (primary key)
- username
- password
- name
- phoneNumber
- address
- detailAddress
- zipcode
- regDate
- isEmailVerified

```
create table user (
  id bigint not null auto_increment primary key,
  name varchar(50) not null,
  username varchar(100) not null,
  password varchar(100) not null,
  phone_number varchar(20) not null,
  address varchar(50) not null,
  detail_address varchar(50) not null,
  zipcode varchar(20) not null,
  reg_date datetime not null default CURRENT_TIMESTAMP,
  is_email_verified int default 0
);
```

### (2) Goods
- id (primary key)
- name
- categoryId (foreign key)
- price
- stock
- description
- imgUrl
- regDate

```
create table goods (
  id bigint not null auto_increment primary key,
  name varchar(50) not null,
  categoryId bigint not null,
  price int not null,
  stock int not null,
  description varchar(255) null,
  imgUrl varchar(255) null,
  reg_date datetime not null default CURRENT_TIMESTAMP
);
```

### (3) Goods Category
- id (primary key)
- name
- categoryIdRef (foreign key)

```
create table goods_category (
  id bigint not null auto_increment primary key,
  name varchar(50) not null,
  categoryIdRef bigint null,
  foreign key(categoryIdRef) references goods_category(id)
);

alter table goods add constraint fk_goods_category foreign key (categoryId) references goods_category(id);
```

## 2. Set a Package Structure (domain, persistence, service, controller)
- domain : a package for VO (Value Objects)
- persistence : a package for DAO (Data Access Objects)
- service : DAO와 Controller를 연결하고 주요 서비스 로직이 들어간다.
- controller : end-point (요청된 url)에 해당하는 서비스를 연결시킨다.

## 3. Create Value Objects in domain package

### (1) UserVO

```
@Getter
@Setter
public class UserVO {
    private Long id;
    private String username;
    private String password;
    private String name;
    private String phoneNumber;
    private String address;
    private String detailAddress;
    private String zipcode;
    private Timestamp regDate;
    private Integer isEmailVerified;
}
```

### (2) GoodsVO

```
@Getter
@Setter
public class GoodsVO {
    private Long id;
    private String name;
    private Long categoryId;
    private int price;
    private int stock;
    private String description;
    private String imgUrl;
    private Timestamp regDate;
}
```

### (3) GoodsCategoryVO

```
@Getter
@Setter
public class GoodsCategoryVO {
    private Long id;
    private String name;
    private Long categoryIdRef;
    private int level;
}
```
