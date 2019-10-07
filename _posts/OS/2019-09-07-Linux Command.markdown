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
  - d (directory) : 디렉터리 자체의 정보 출력
  - i (inode) : 파일의 inode 번호 출력
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

- 파일 이름이나 속성을 이용하여 해당하는 파일 찾기 : `$ find [directory] -[options]`
  - 옵션의 검색 조건에 따라 지정된 디렉터리 아래에서 해당되는 파일들을 모두 찾아 출력
  - 검색 조건 (조합 가능)
    - `-name [file]` : 파일명으로 검색
    - `-atime +n` : 접근 시간이 n일 이전(x > n)인 파일 검색
    - `-atime -n` : 접근 시간이 n일 이내인 파일 검색
    - `-mtime +n` : n일 이전에 수정된 파일 검색
    - `-mtime -n` : n일 이내에 수정된 파일 검색
    - `-perm nnn` : 접근 권한이 nnn인 파일 검색
    - `-type x` : 파일 종류가 x인 파일 검색
    - `-size n` : 파일 크기가 n 블록(512byte)인 파일 검색
    - `-links n` : 링크 개수가 n인 파일 검색
    - `-user [username]` : 파일의 사용자가 사용자명인 파일 검색
    - `-group [group_name]` : 그룹의 사용자가 그룹명인 파일 검색
    - `-print` : 찾은 파일의 절대 경로명을 출력
    - `-ls` : 찾은 파일에 대해 ls -dils 명령어 실행 결과 출력
      - `ls -dils` : 파일들이 존재하는 디렉토리 자체의 정보와 파일의 inode 번호, 상세 정보, 크기를 출력
    - `-exec cmd {};` : 찾은 파일들에 대해 cmd 명령어를 실행

- `$ grep [pattern] [file]` : 파일들을 대상으로 지정된 패턴의 문자열을 검색하고, 해당 문자열을 포함하는 줄들을 출력
  - ![grep](../../assets/OS/34.PNG)
  - 옵션
    - i : 대소문자 무시
    - l : 해당 패턴이 들어있는 파일 이름을 출력
    - n : 각 줄의 줄 번호 출력
    - v : 명시된 패턴을 포함하지 않는 줄을 출력
    - c : 패턴과 일치하는 줄 수 출력
    - w : 패턴이 하나의 단어로 된 것만 출력
  - Regular Expression
    - ? : 0 or 1
      - 'ab?' : 'ab' 혹은 ab 다음에 한 글자가 오는 문자열
    - . : 1 character
      - 'a...b' : a로 시작해서 b로 끝나는 길이 5 문자열
    - \* : 바로 앞의 문자를 0번 이상 반복
      - 'a*b' : b, ab, aab, aaab, ...
    - [] : 대괄호 사이의 문자 중 하나
      - \- : 문자의 범위를 지정
      - '[abc]d' : ad, bd, cd
      - '[a-z]' : a부터 z 중 하나
    - [^...] : [^ ] 사이의 문자를 제외한 나머지 문자 중 하나
      - '[^abc]d' : ad, bd, cd를 제외한 나머지 (ed, fd, ..., zd)
      - '[^a-z] : 소문자 알파벳을 제외한 나머지 문자 중 하나
    - ^ : 줄의 시작
      - '^string' : 해당 문자열로 시작하는 줄
    - $ : 줄의 끝
      - 'string$' : 해당 문자열로 끝나는 줄
  - 파이프(|)와 함께 grep 사용 : 어떤 명령어를 실행하고 난 결과 중에서 원하는 단어 혹은 문자열 패턴을 찾고자 할 때 사용

- 정렬 : `$ sort -[options] [files]`
  - 텍스트 파일(들)의 내용을 줄 단위로 옵션에 따라 다양한 형태로 정렬
  - 정렬 필드를 기준으로 줄 단위로 오름차순으로 정렬
  - 기본적으로는 각 줄의 첫 번째 필드가 정렬 필드
  - 옵션
    - b : 앞에 붙는 공백 무시
    - c : 정렬되지 않은 상태로 출력
    - d : 숫자, 문자, 공백만 비교하여 사전순으로 출력
    - f : 대소문자를 구분하지 않고 정렬
    - n : 숫자 문자열의 숫자 값에 따라 비교하여 정렬
    - r : 내림차순
    - t [character] : 지정한 문자를 필드 구분자로 사용
    - o [file] : 정렬된 내용을 지정된 파일에 저장
    - k [field_number] : 필드 번호에 해당하는 필드를 기준으로 정렬 (필드 번호는 1부터 시작)
    - \+ [start_field_number] \- [end_field_number] : 시작 필드 번호부터 종료 필드 번호-1까지의 필드들을 정렬 (필드 번호는 0부터 시작)

- 파일 비교 (compare) : `$ cmp [file1] [file2]`
  - file1와 file2가 같은지 비교
  - 두 파일이 같으면 아무 것도 출력하지 않고 다르면 서로 달라지는 위치를 출력
- 파일 비교 (difference) : `$ diff [-i] [file1] [file2]`
  - file1과 file2를 줄 단위로 비교하여 차이점을 출력
  - i 옵션은 대소문자를 무시
  - file1을 file2의 내용과 같도록 바꿀 수 있는 편집 명령어 형태로 출력한다.
  - 편집 명령어
    - a (추가) : [file1_line_number] a [file2_line_number1] [file2_line_number2]
      - file1의 줄 번호 이후에 file2의 줄 번호 1부터 2까지의 줄들을 추가하면 두 파일은 서로 같다.
    - d (삭제) : [file1_line_number1] [file1_line_number2] d [file2_line_number]
      - file1의 줄 번호 1부터 2까지 삭제하면 file2의 줄 번호 이후와 두 파일은 서로 같다.
    - c (변경) : [file1_line_number1] [file1_line_number2] c [file2_line_number1] [file2_line_number2]
      - file1의 줄 번호 1부터 2까지의 내용을 file2의 줄 번호 1부터 2까지의 내용으로 대치하면 두 파일은 서로 같다.

- 파일 분할 : `$ split [-l n] [input_file] [output_file]`
  - 하나의 입력 파일을 일정한 크기의 여러 개 작은 파일로 분할한다. -l n 옵션으로 분할할 줄 수를 n으로 지정할 수 있다.

- 파일 합병 (concatenation) : `$ cat [file1] [file2] > [file3]`
  - file1과 file2의 내용을 붙여서 새로운 file3을 만든다.

- 파일 합병 (paste) : `$ paste [-s] [-d [seperated_character]] [file]`
  - 여러 파일들을 줄 단위로 합병하여 하나의 파일을 만든다.
  - s 옵션은 한 파일 끝에 다른 파일의 내용을 덧붙인다.