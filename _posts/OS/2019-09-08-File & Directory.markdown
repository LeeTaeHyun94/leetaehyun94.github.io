---
layout: post
title: "Linux Command"
description: "Linux Command"
date: 2019-09-07 13:25:00
categories: OS
comments: true
---

# 1. 파일의 종류
- 일반 파일 (Ordinary File) 
  - 데이터를 가지고 있으면서 디스크에 저장된다.
  - 텍스트 파일, 이진 파일
- 디렉터리 또는 폴더
  - 파일들을 계층적으로 조직화하는데 사용되는 일종의 특수 파일
  - 디렉터리 내에 파일이나 서브 디렉터리들이 존재
- 장치 파일 (Device Special File)
  - 물리적인 장치에 대한 내부적 표현
  - 키보드(stdin), 모니터(stdout), 프린터 등도 파일처럼 사용
- 심볼릭 링크 파일
  - 어떤 파일을 가리키는 또 하나의 경로명을 저장하는 파일

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