---
layout: post
title: "Linux Command"
description: "Linux Command"
date: 2019-09-07 13:25:00
categories: OS
comments: true
---

# 1. 파일의 종류
- 일반 파일 (Ordinary File -)
  - 데이터를 가지고 있으면서 디스크에 저장된다.
  - 텍스트 파일, 이진 파일
- 디렉터리 또는 폴더 (d)
  - 파일들을 계층적으로 조직화하는데 사용되는 일종의 특수 파일
  - 디렉터리 내에 파일이나 서브 디렉터리들이 존재
- 장치 파일 (Device Special File)
  - 물리적인 장치에 대한 내부적 표현
  - 키보드(stdin), 모니터(stdout), 프린터 등도 파일처럼 사용
  - 문자 장치 파일 (c) : 문자 단위로 데이터를 전송하는 장치를 나타내는 파일
  - 블록 장치 파일 (b) : 블록 단위로 데이터를 전송하는 장치를 나타내는 파일
- 심볼릭 링크 파일 (l)
  - 다른 파일을 가리키고 있는 별도의 파일
  - 실제 파일의 경로명을 저장하고 있는 일종의 특수 파일
  - 어떤 파일을 가리키는 또 하나의 경로명을 저장하는 파일
- > 하드 링크 (파일은 아님) : 기존 파일에 대한 새로운 이름이라고 할 수 있다. 실제로 기존 파일을 대표하는 i-node를 가리켜 구현
- FIFO 파일 (p) : 프로세스 간 통신에 사용되는 이름 있는 파이프
- 소켓 (s) : 네트워크를 통한 프로세스 간 통신에 사용되는 파일

# 2. 디렉터리 계층 구조
- 리눅스의 디렉터리는 루트로부터 시작하여 트리 형태의 계층 구조를 이룬다.
![Directory Hierarchy Structure](../../assets/OS/21.PNG)

# 3. 홈 디렉터리
- 각 사용자마다 별도의 홈 디렉터리가 있음
- 사용자가 로그인하면 홈 디렉터리에서 작업을 시작한다.
![Home Directory](../../assets/OS/22.PNG)

# 4. 경로명
- 파일이나 디렉터리에 대한 정확한 이름
- 절대 경로명 (Absolute Path Name) : 루트 디렉터리부터 시작하여 경로 이름을 정확하게 적는 것
- 상대 경로명 (Relative Path Name) : 현재 작업 디렉터리부터 시작해서 경로 이름을 적는 것
![Path Name](../../assets/OS/23.PNG)

# 5. 파일 속성 (File Attribute)
- 파일 크기, 종류, 접근 권한, 링크 수, 소유자 및 그룹, 수정 시간
- ```
  $ ls -sl cs1.txt
  4 – rw-rw-r-- 1 chang cs 2088 4월 16일 13:37 cs1.txt
  ```
  - 파일 크기 4(KB)
  - 파일 종류 - : 일반 파일(-), 디렉터리(d), 링크(l), 파이프(p), 소켓(s), 디바이스(b or c)...
  - 접근 권한 rw-rw-r-- : 파일에 대한 소유자, 그룹, 기타 사용자의 읽기(r)/쓰기(w),실행(x) 권한
  - 하드 링크 수 1 : 파일에 대한 하드 링크 개수
  - 소유자 및 그룹 chang cs : 파일의 소유자 ID 및 소유자가 속한 그룹
  - 파일 크기 2088(Byte)
  - 최종 수정 시간 4월 16일 13:37 : 파일을 생성 혹은 마지막으로 수정한 시간
  - 파일 이름 cs1.txt

# 6. 파일 접근 권한 (File Permission Mode)
- ![File Permission Mode](../../assets/OS/24.PNG)
- 소유자(owner)/그룹(group)/기타(others)로 구분하여 관리한다.
  - 예 : rwxr-xr-x (755)
    - ![File Permission Mode](../../assets/OS/25.PNG)
  - ![File Permission Mode Example](../../assets/OS/26.PNG)
