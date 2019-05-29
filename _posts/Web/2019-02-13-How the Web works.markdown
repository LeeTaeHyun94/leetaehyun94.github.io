---
layout: post
title:  "How the Web works"
description: "How the Web works"
date:   2019-02-13 01:00:00
categories: Web
comments: true
---
## 1. Client & Server
웹에 연결된 컴퓨터는 클라이언트와 서버, 두 가지 종류로 나눌 수 있다.
- 클라이언트 : 일반적인 웹 사용자의 인터넷이 연결된 장치들과 이런 장치들에서 이용 가능한 웹에 접근하는 소프트웨어
- 서버 : 웹 페이지, 사이트, 앱을 저장하는 컴퓨터

## 2. Component for Web
(1) 인터넷 연결 : 웹에서 데이터를 보내고 받을 수 있게 하는 원동력
(2) TCP/IP (Transmission Control Protocol/Internet Protocol) : 데이터가 목적지를 향해 어떻게 웹을 지나다닐 수 있는지 정의하는 통신 규약
(3) DNS (Domain Name System Servers) : 웹 사이트를 위한 주소록
  - IP 주소는 정확히 기억하기에 쉽지 않기 때문에 특정 도메인을 지정하고 도메인에 따라 웹 사이트의 IP 주소로 매칭시켜준다.

(4) HTTP (HyperText Transfer Protocol) : 클라이언트와 서버가 서로 통신할 수 있게 하기 위한 언어를 정의하는 Application Protocol
(5) Component Files :  웹 사이트를 구성하는 여러 파일들
  - Codes : 근본적으로는 HTML, CSS, Javascript로 구성되어 있다.
  - Resources : 이미지, 음악, 비디오 등등 웹 사이트를 구성하는 코드를 제외한 요소들

## 3. Workflow of Web in Browser
(1) 브라우저에 웹 사이트 주소를 입력한다.

(2) 브라우저는 DNS Server에 접근해 웹 사이트가 존재하는 서버의 IP 주소를 찾는다.

(3) 브라우저는 서버에 웹 사이트의 사본을 클라이언트에게 보내달라는 HTTP Request 메시지를 전송한다. (클라이언트와 서버 사이의 모든 데이터는 TCP/IP 연결을 통해서 전송된다.)

(4) 서버는 요청 메시지를 받고 클라이언트의 요청을 승인하고 처리에 대한 결과(응답)를 전송한다. 정상적인 흐름이면, 서버는 웹 사이트의 파일들을 데이터 패킷으로 브라우저에 전송한다.

(5) 브라우저는 전송받은 데이터 패킷을 조합하여 하나의 웹 페이지를 구성한다.