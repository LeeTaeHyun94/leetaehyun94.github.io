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

- 로그인 쉘 변경 (change shell) : `chsh`

- 쉘 지역 변수 설정 : `$ [variable name]=[value(string)]`
  - 지역 변수는 현재 사용 중인 터미널에서만 사용가능하다.

- 환경 변수 보기 : `env`

- 쉘 환경 변수 설정 : `$ export [variable name]=[value(string)]`
  - 환경 변수는 시스템 전체에 적용된다.

- 전면 처리 : `$ [command]`

- 후면 처리 : `$ [command] &`

- 후면 작업 확인 : `$ jobs [job number]`
  - 작업 번호를 넣지 않으면 현재 실행 중인 전체 작업 목록을 출력한다.

- 후면 작업을 전면 작업으로 전환 : `$ fg [job number]`

- 출력 재지정 (output redirection) : `$ [command] > [file]`
  - 명령어의 표준 출력을 화면 대신에 파일에 저장한다.

- 출력 추가 : `$ [command] >> [file]`
  - 명령어의 표준 출력을 화면 대신에 파일에 추가한다.

- 입력 재지정 (input redirection) : `$ [command] < [file]`
  - 명령어의 표준 입력을 키보드 대신에 파일에서 받는다.

- 오류 재지정 (output redirection) : `$ [command] 2> [file]`
  - 명령어의 표준 오류를 화면 대신에 파일에 저장한다.

- 프로세스 상태 보기 (process status) : `$ ps -[options]`
  - 현재 시스템 내에 존재하는 프로세스들의 실행 상태를 요약해서 출력한다.
  - ps 출력 정보
    - UID : 프로세스를 실행시킨 사용자 ID
    - PID : 프로세스 번호
    - PPID : 부모 프로세스 번호
    - C : 프로세스의 우선 순위
    - STIME : 프로세스의 시작 시간
    - TTY : 명령어가 시작된 터미널
    - TIME : 프로세스에 사용된 CPU 시간
    - CMD : 실행되고 있는 명령어(프로그램) 이름
  - 옵션 (각 계열에 따라 일반적으로 많이 이용하는 옵션이 있다.)
    - BSD 계열인 경우
      - a : 모든 사용자의 프로세스를 출력
      - u : 프로세스에 대한 자세한 정보를 출력
      - x : 더 이상 제어 터미널을 갖지 않는 프로세스들도 함께 출력
    - 시스템 V 계열인 경우
      - e : 현재 시스템 내에 실행 중인 모든 사용자의 프로세스 정보를 출력
      - f : 프로세스에 대한 자세한 정보를 출력

- 특정 프로세스 리스트 : `$ pgrep -[options] [pattern]`
  - 패턴에 해당하는 프로세스들만을 리스트한다.
  - 옵션
    - l : PID와 함께 프로세스 이름을 출력한다.
    - f : 명령어의 경로도 출력한다.
    - n : 패턴과 일치하는 프로세스들 중에서 가장 최근 프로세스만 출력한다.
    - x : 패턴과 정확하게 일치되는 프로세스만 출력한다.

- 쉘 재우기 : `$ sleep [seconds]`
  - 명시된 시간만큼 프로세스 실행을 중지시킨다.

- 강제 종료 : `Ctrl-C`

- 실행 중지 : `Ctrl-Z`

- 후면 작업의 전면 전환 (foreground) : `$ fg %[JobID]`

- 전면 작업의 후면 전환 (background) : `$ bg %[JobID]`
  - 작업 번호에 해당하는 중지된 작업을 후면 작업으로 전환하여 실행한다.
  - 전면 실행 중인 작업을 `Ctrl-Z`키로 실행 중지시킨 후 bg 명령어를 사용한다.

- 후면 작업의 입출력 제어
  - 후면 작업의 출력 : `$ [command] > [output file] &`
    - ex)
      - find . -name test.c -print > find.txt &
      - find . -name test.c -print | mail [user] &
  - 후면 작업의 입력 : `$ [command] < [input file] &`

- 프로세스 끝내기 : `$ kill [PID]`, `$ kill %[JobID]`
  - PID 혹은 작업 번호에 해당하는 프로세스를 강제로 종료한다.

- 프로세스 기다리기 : `$ wait [PID]`
  - 프로세스 번호로 지정한 자식 프로세스가 종료될 떄까지 기다린다. 지정하지 않으면 모든 자식 프로세스가 종료되기를 기다린다.

- 로그아웃 후에도 프로세스 실행하기 : `$ nohup [command] [parameter] &`
  - 로그아웃 후에도 명령어 실행이 끝날 때까지 실행한다.
  - 명령어의 결과는 화면(표준 출력)에는 출력되지 않고 시스템 내의 nohup.out이라는 파일에 기록된다.

- 프로세스 우선순위
  - nice 값으로 실행의 우선순위를 정한다.
    - 작은 숫자일수록 우선순위가 높다. (19 ~ -20)
    - 일반적으로 기본값은 0이다.
  - `$ nice -n [value(19~-20)] [command] [parameter]` : 주어진 명령을 조정된 우선순위로 실행
  - `$ renice -n [value(19~-20)] -[gpu] [PID]` : 이미 수행 중인 프로세스의 우선순위를 명시된 우선순위로 변경한다.
    - 옵션
      - g : 해당 그룹 소유로 된 프로세스를 의미한다.
      - u : 지정한 사용자의 소유로 된 프로세스를 의미한다.
      - p : 해당 프로세스의 PID를 지정한다.

- `$ id [UID]` : 사용자의 실제 ID와 유효 사용자 ID, 그룹 ID 등을 보여준다.

- 시그널 리스트 : `$ kill -l`

- 시그널 보내기 : `$ kill -[signal] [PID]`, `$ kill -[signal] [JobID]`
  - PID 혹은 작업 번호로 지정된 프로세스에 원하는 시그널을 보낸다. 시그널을 명시하지 않으면 SIGTERM 시그널을 보내 프로세스를 강제 종료한다.

- 호스트명 : `$ hostname`
  - 사용 중인 시스템의 호스트명을 출력

- IP 주소 : `$ ip addr`
  - 사용 중인 시스템의 IP 주소를 출력

- `$ nslookup [hostname]` (name server lookup)
  - 지정된 호스트의 IP 주소를 얄려준다.
  - 도메인 이름 서버(DNS, Domain Name Server)에 호스트명에 대해 질의

- 사용자 정보 : `$ finger [username]`
  - 지정된 사용자에 대한 보다 자세한 정보를 알려준다.

- 메시지 보내기 : `$ write [username] [terminal_name]`
  - 현재 로그인되어 있는 다른 사용자에게 메시지를 보낸다.

- 전체 메시지 (write all) : `$ wall [file]`
  - 현재 로그인되어 있는 모든 사용자에게 메시지를 보낸다.
  - 파일 내용도 메시지로 보낼 수 있다.

- ftp 명령어를 이용하여 파일 전송 : `$ ftp -n [hostname]`
  - 호스트명으로 지정된 FTP 서버에 접속하여 파일을 업로드/다운로드한다.
  - ftp 내부 명령어
    - `!command` : 로컬 호스트에서 명령어 실행
    - `lcd path` : 로컬 호스트의 작업 디렉토리 변경
    - `cd path` : 원격 호스트의 작업 디렉토리 변경
    - `get [file]` : 해당 파일을 다운로드
    - `mget [file1, file2, ...]` : 여러 파일들을 다운로드한다. 대표 문자 사용 가능
    - `put [file]` : 해당 파일을 업로드
    - `mput [file1, file2, ...]` : 여러 파일들을 업로드한다. 대표 문자 사용 가능
    - `help` : 도움말
    - `ls [path]` : 원격 호스트의 해당 디렉토리 리스트
    - `pwd` : 원격 호스트에서 현재 작업 디렉토리 출력
    - `quit` : 종료
    - `ascii` : 전송 모드를 아스키 모드(ascii mode)로 설정 (기본 설정이며 텍스트 파일 전송 시 사용)
    - `bin` : 전송 모드를 바이너리 모드(binary mode)로 설정 (실행 파일, 이진 파일 전송 시 사용)

- sftp 명령어를 이용하여 파일 전송 : `$ sftp -n [hostname]`
  - 호스트명으로 지정된 SFTP 서버에 접속하여 파일을 업로드/다운로드한다.

- `$ telnet [hostname]`, `$ telnet [ip_address]` : 지정된 원격 호스트에 원격으로 접속한다.

- `$ ssh [username]@[hostname]`, `$ ssh -l [username] [hostname]` : 지정된 원격 호스트에 사용자명으로 원격 접속한다.

- 원격 명령 실행 : `$ ssh [hostname] [command]`

- 원격 컴퓨터의 상태를 확인 : `$ ping [hostname]`
  - IP 네트워크를 통해 지정된 원격 호스트가 도달 가능한지 테스트하여 상태를 확인