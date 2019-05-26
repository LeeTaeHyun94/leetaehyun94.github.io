---
layout: post
title: "System Call"
description: "System Call"
date: 2019-05-26 18:20:00
categories: OS
comments: true
---
커널 영역의 기능을 사용자 모드가 사용 가능하게, 사용자 어플리케이션이 커널 내부 하드웨어나 데이터에 간접적으로 접근해서 요구하는 기능을 수행하는 시스템 호출 인터페이스
![open System Call Process](../../assets/OS/17.PNG)

## 1. 유형
(1) 프로세스 제어 (Process Control)
- 종료(end), 중지(abort)
- 적재(load), 실행(execute)
- 프로세스 생성 (create)
- 프로세스 속성 획득 및 설정 
- 시간 대기 (wait time)
- 사건 대기 (wait event)
- 사건 알림 (signal event)
- 메모리 할당 및 해제 (malloc/free)

(2) 파일 조작 (File Manipulation)
- 파일 생성 및 삭제 (create/delete)
- 열기/닫기 (open/close)
- 읽기/쓰기/위치 변경 (read/write/reposition)
- 파일 속성 획득 및 설정 (getter/setter for file attribute)

(3) 장치 관리 (Device Management)
- 장치 요구 및 방출 (request/release device)
- 읽기/쓰기/위치 변경 (read/write/reposition)
- 장치 속성 획득 및 설정 (getter/setter for device attribute)
- 장치의 논리적 부착/분리 (attach/detach)

(4) 정보 유지 (Information Maintenance)
- 시간, 날짜 설정 및 획득 (time)
- 시스템 데이터 설정 및 획득 (date)
- 프로세스, 파일, 장치 속성 획득 및 설정

(5) 통신 (Communication)
- 통신 연결의 생성 및 제거
- 메시지의 송수신
- 상태 정보 전달
- 원격 장치의 부착 및 분리
메시지 전달과 공유 메모리 두 가지 모델을 통해 통신한다.
메시지 전달 모델에서는 프로세스 간 통신을 이용하여 메시지를 주고 받고, 공유 메모리 모델에서는 다른 프로세스에 할당된 메모리에 접근을 위해 특정 시스템 호출을 이용한다.
