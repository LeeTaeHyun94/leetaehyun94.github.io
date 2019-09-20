---
layout: post
title: "Linux Command"
description: "Linux Command"
date: 2019-09-07 13:25:00
categories: OS
comments: true
---

- 날짜 및 시간 확인 : `date`

- 시스템 정보 확인
  - `hostname`
  - `uname`
    - 옵션 -a

- 사용자 정보 확인
  - 사용자 목록 : `who`
  - 현재 사용자 : `whoami`

- 디렉터리 내용 확인 : `ls`

- 패스워드 변경 : `passwd`

- 화면 정리 : `clear`

- 온라인 매뉴얼 : `man`

- 명령어에 대한 간단한 설명 : `whatis`

- 현재 작업 디렉터리 출력 : `pwd` (print working diretory)

- 디렉터리 이동 : `cd [directory]` (change directory)

- 명령어의 경로 확인 : `which [command]`

- 디렉터리 리스트 : `ls(or dir) [-aslFR] [directory or file]` (list)
  - a (all) : 숨겨진 파일을 포함하여 모든 파일을 리스트한다.
  - s (size) : 파일의 크기를 KB 단위로 출력
  - l (long) : 파일의 상세 정보를 출력
  - F : 파일의 종류를 표시하여 출력
  - R (Recursive) : 모든 하위 디렉터리들을 리스트한다.

- 디렉터리 생성 : `mkdir [-p] [directory]` (make directory)
  - p : 중간 디렉터리 자동 생성 옵션

- 디렉터리 삭제 : `rmdir [directory]` (remove directory)
  - 빈 디렉터리만 삭제 가능할 수 있다.

- GNOME이 제공하는 GUI 기반 문서 편집기 : `gedit [file] &`

- 표준 입력 내용을 모두 파일에 저장 : `cat > [file]`
  - 파일이 없으면 새로 생성

- 파일 크기가 0인 이름만 있는 빈 파일 생성 : `touch [file]`
  - 이미 존재하는 파일의 경우 해당 파일의 최종 사용 시간과 수정 시간을 현재 시간으로 변경한다.

- 파일 내용을 화면에 그대로 출력 : `cat [-n] [file]`
  - 파일을 지정하지 않으면 표준 입력 내용을 화면에 그대로 출력한다.

- 파일 내용을 페이지 단위로 화면에 출력 : `more [file]`

- 파일의 앞부분을 화면에 출력 : `head [-n] [file]`
  - 파일을 지정하지 않으면 표준 입력 내용을 대상으로 한다.

- 파일의 뒷부분을 화면에 출력 : `tail [-n] [file]`
  - 파일을 지정하지 않으면 표준 입력 내용을 대상으로 한다.

- 파일에 저장된 줄(l), 단어(w), 문자(c)의 개수를 출력 : `wc [-lwc] [file]` (word count)
  - 파일을 지정하지 않으면 표준 입력 내용을 대상으로 한다.

- 파일 복사 (copy)
  - ```
    $ cp [file 1] [file 2] // file 1을 file 2에 복사
    $ cp [file] [directory] // file을 지정된 directory에 복사
    $ cp [file 1] ... [file n] [directory] // 여러 개의 file을 지정된 directory에 복사
    $ cp -r [directory 1] [directory 2] // r(recursion) 옵션을 사용해 directory 1 전체를 directory 2에 복사 (하위 디렉터리를 포함하여 복사)
    ```
  - i : 대화형 옵션 (명령을 수행할 것인지 한 번 더 확인)
  - 복사 대상 파일과 이름이 같은 파일이 이미 존재하면 덮어쓰기

- 파일 이동 (move)
  - ```
    $ mv [file] [directory] // file을 지정된 directory로 이동
    $ mv [file 1] ... [file n] [directory] // 여러 개의 file을 지정된 directory로 이동
    $ mv [directory 1] [directory 2] // directory 1을 directory 2로 이름 변경
    ```
  - i : 대화형 옵션
  - 이동 대상 파일과 이름이 같은 파일이 이미 존재하면 덮어쓰기

- 파일 삭제 (remove)
  - ```
    $ rm [file] // 파일 삭제
    $ rm -r [directory] // 디렉터리 전체 삭제
    ```
  - i : 대화형 옵션

- 링크 (link)
  - ```
    $ ln [-s] [file 1] [file 2] // file 1에 대한 새로운 이름(링크)으로 file 2 생성
    $ ln [-s] [file] [directory] // file에 대한 링크를 지정된 디렉터리에 같은 이름으로 생성
    ```
  - s : 이 옵션을 붙이면 심볼릭 링크 파일, 없으면 하드 링크

- 파일의 종류에 대한 자세한 정보 출력 : `file [file]`

- 접근 권한 변경 (change mode)
  - ```
    $ chmod [-R] [permission mode] [file or directory] // 파일 혹은 디렉터리의 접근 권한을 변경
    ```
  - R : 지정된 디렉터리 내 모든 파일과 디렉터리에 대해서도 접근 권한을 변경할 수 있는 옵션
  - 접근 권한 표현
    - 8진수
      - ![Permission Mode Expression - Octal Number](../../assets/OS/27.PNG)
    - 기호
      - ![Permission Mode Expression - Figure](../../assets/OS/28.PNG)
      - 예시
        - ![Change Permission Mode Expression Example - Figure](../../assets/OS/29.PNG)

- 소유자 변경 (change owner)
  - ```
    $ chown [-R] [user] [file or directory] // 파일 혹은 디렉터리의 소유자를 지정된 사용자로 변경
    ```
  - R : 지정된 디렉터리 내 모든 파일과 디렉터리에 대해서도 소유자를 변경할 수 있는 옵션

- 그룹 변경 (change group)
  - ```
    $ chgrp [-R] [group] [file or directory] // 파일 혹은 디렉터리의 그룹을 지정된 그룹으로 변경
    ```
  - R : 지정된 디렉터리 내 모든 파일과 디렉터리에 대해서도 그룹을 변경할 수 있는 옵션

- 쉘 변경
  - /bin 디렉터리 경로는 환경 변수로 지정되어 있으므로 변경할 쉘의 이름만 입력하여 실행하면 된다.
  - 본 쉘 (sh), 콘 쉘 (ksh), Bash 쉘 (bash), C 쉘 (csh), tcsh

- 로그인 쉘 변경 (change shell) : chsh