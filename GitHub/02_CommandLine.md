# 02. Command Line (1)

### 들어가며
01. <a href="#definitions">커널, 셸, 그리고 터미널 프로그램이란?</a>
02. <a href="#popular-use">자주 사용하는 명령어</a>
    1. [pwd](#pwd)
    2. [cd](#cd)
    3. [/tmp](#상위-디렉터리,-홈-디렉터리,-임시-디렉터리-/tmp)
    4. [ls](#ls)
03. <a href="#control">파일, 디렉터리 조작을 위한 기본 명령어</a>
    1. [mkdir](#mkdir)
    2. [touch](#touch)
    3. [mv](#mv)
    4. [cp](#cp)
    5. [rm](#rm)
04. <a href="#print">문자열 출력, 파일과 관련된 셸 기본 명령어 모음</a>
    1. [echo](#echo)
    2. [cat](#cat)
    3. [head](#head)
    4. [tail](#tail)
05. <a href="#help">사용법과 매뉴얼</a>
    1. [-h, --help](#--help)
    2. [man](#man)
06. <a href="#option">왜 어떤 옵션은 –를 사용하고 어떤 옵션은 ––를 사용하나요?</a>
07. <a href="#escape">서바이벌 가이드: 비상 탈출 버튼 ^c, ^d, ^\, ^z</a>



***

<h2 id="definitions">커널, 셸, 그리고 터미널 프로그램이란?</h2>
각 용어에 대한 한 줄 정의
 - 커널   : 운영체제 중 항상 메모리에 올라가 있는 운영체제의 핵심 부분으로써 하드웨어와 응용 프로그램 사이에서 인터페이스를 제공 및 컴퓨터 자원을 관리하는 역할을 하는 프로그램
 - 셸     : 커맨드라인 인터페이스로 터미널에서 실행할 수 있으며 운영체제 커널에 명령을 내릴 수 있는 인터렉티브 프로그램
 - 터미널 : 커맨드라인 인터페이스가 물리적으로 구현된 기계

***

## <h2 id="popular-use">자주 사용하는 명령어</h2>
## pwd
`$ pwd`
 - Print Working Directory
 - 현재 디렉터리를 출력해 주는 명령어
 
## cd
`$ cd <DIR>`
 - Change Directory
 - 디렉터리로 이동
 - `<DIR>`에는 이동하고자 하는 위치를 지정 

### 현재 디렉터리 표현법, 절대 경로와 상대 경로
1. 셸에서는 현재 디렉터리를 `.`, 루트 디렉터리를 `/`로 나타냄
   - `$ cd .` : 현재 디렉터리에서 현재 디렉터리로 이동
   - `$ cd ./directory01` : 현재 디렉터리 내의 'directory01' 디렉터리로 이동
   - `$ cd directory01` : 현재 디렉터리 내의 'directory01' 디렉터리로 이동 (즉, `./`생략 가능)

### 상위 디렉터리, 홈 디렉터리, 임시 디렉터리 /tmp
1. 셸에서는 상위 디렉터리를 `..` 로 나타냄
   - `$ cd ..` : 현재 디렉터리의 상위 디렉터리로 이동
   - `$ cd ../..` : 현재 디렉터리의 상위 디렉터리의 상위 디렉터리로 이동

2. 셸에서 `~`(틸데)는 현재 셸 프로세스를 실행한 사용자의 홈 디렉터리를 의미함
    ```
    $ cd ~
    $ pwd
    /c/Users/eunss
    ```

3. 임시로 사용되는 디렉터리 /tmp
   ```
   $ cd /tmp
   $ pwd
   /tmp
   ```
   - /tmp에 저장한 작업 내용은 재부팅 시 사라질 수 있으므로 주의가 필요함
   - 관리자 권한이 아닌 경우 루트 아래의 다른 디렉터리에 접근이 불가한 경우도 있음

4. 셸에서 현재 사용자를 확인할 때는 `$ whoami` 명령어를 사용함
    ```
    $ whoami
    Emma
    ```
   
## ls
`$ ls`

- list   
- 옵션
  - `$ ls -g` : 타입에 따라서 다른 색으로 출력
    - 흰색 : 파일
    - 하늘색 : 디렉터리
    - 보라색 : 다른 곳에 연결된 파일
  - `$ ls -d */` : 디렉터리만 출력
  - `$ ls -l` : 자세한 정보 표시
  - `$ ls -a` : 숨김 파일 표시
  - `$ ls -R` : 위치한 디렉터리의 하부 디렉터리의 파일까지 모두 출력
  - `$ ls -r` : 출력 결과를 내림차순으로 정렬
  - `$ ls -t` : 출력 결과를 파일이 수정된 시간을 기준으로 정렬
  - ... 참고 - [[Linux] 리눅스 ls 명령어 사용법 & 옵션 정리 (디렉터리 목록 확인)](https://coding-factory.tistory.com/748)

***

<h2 id="control">파일, 디렉터리 조작을 위한 기본 명령어</h2>
## mkdir
`$ mkdir <DIR>`

- MaKe a DIRectory
- 디렉터리 생성
- `<DIR>`에는 생성하고자 하는 디렉터리 이름을 지정
- 옵션 `-p`
```
$ cd ~
$ mkdir -p hello/world
$ cd hello/world
$ pwd
/c/Users/eunss/hello/world
```

## touch
`$ touch <file name>`
 - 이미 존재하는 파일의 접근 시간 혹은 수정 시간을 변경하는 명령어 (원래 용도)
 - 빈 파일 생성 명령어
 - 여러 개 파일을 한꺼번에 만들 수 있음
    
    ```
    $ touch a b c d e
    $ ls
    a  b  c  d  e  world/
    ```

## mv
`$ mv <SRC> <DEST>`
 - MoVe source to destination
 - [SRC]는 이동하고자 하는 파일의 경로, [DEST]는 새로운 경로를 의미
  ```
  ./hello: [a  b  c  d  e  world/]
  ```
  ```
  $ mv a world/
  $ ls -R
  .:
  b  c  d  e  world/
   
  ./world:
  a
  ```
 - 특정 파일의 상위 폴더 이동 : `$ mv a ../` 이동할 경로에 상위 폴더를 지정

 - 이름 변경
  ```
  ./hello: [b  c  d  e  world/]
  ```
  ```
  $ mv c cat
  $ ls -R
  b  cat  d  e  world/
  ```

## cp
`$ copy <SRC> <DEST>`
 - CoPy source to destination
 - SRC는 복사하고자 하는 파일의 경로, DEST는 새로운 경로를 의미

  ```
  ./hello: [ b  cat  d  e  world/]
  ./world: [a]
  ```
  ```
  $ cp b e world/
  $ ls -R
  .:
  b  cat  d  e  world/
   
  ./world:
  a  b  e
  ```
 - 복사 및 이름 변경
  ```
  ./hello: [b  cat  d  e  world/]
  ```
  ```
  $ cp d dragon
  $ ls
  b  cat  d  dragon  e  world/
  ```

## rm
`$ rm <file or directory/>`
 - ReMove a file, files or directory
  ```
  [b  cat  d  dragon  e  world/]
  ```
  ```
  $ rm b cat e
  $ ls
  d  dragon  world/
  ```
 - 옵션 
   - `-r` : 디렉터리 삭제 시 하위 경로의 파일을 삭제하는 옵션
   - `-f` : 파일, 디렉터리 삭제 시 강제로 삭제하는 옵션
   - `-v` : 파일, 디렉터리 삭제 후 결과를 보여주는 옵션
 - `$ rm -rf <file or directory/>` 형태로 많이 쓰임

***

<h2 id="print">문자열 출력, 파일과 관련된 셸 기본 명령어 모음</h2>
## echo
 - 화면에 문자열을 출력
```
$ echo Hello, world!
Hello, world!
```
```
$ echo My home directory is $HOME.
My home directory is /Users/44bits.
```
 - 커맨드라인에서 동작하는 프로그램을 작성할 때, 화면에 문자열을 출력하는 기본적인 기능
 - 셸 스크립트에서 사용하거나 환경변수 출력에 사용하기도 함

## cat
 - 파일의 전체 내용 출력
```
$ cd /etc
$ cat bash.bashrc
```
```
...
# System-wide bashrc file

# Check that we haven't already been sourced.
([[ -z ${CYG_SYS_BASHRC} ]] && CYG_SYS_BASHRC="1") || return

# If not running interactively, don't do anything
[[ "$-" != *i* ]] && return
...
```

## head
 - 파일의 앞부분 일부를 출력
```
$ cd /etc
$ head bash.bashrc
```
```
# To the extent possible under law, the author(s) have dedicated all 
# copyright and related and neighboring rights to this software to the
# public domain worldwide. This software is distributed without any warranty.
# You should have received a copy of the CC0 Public Domain Dedication along
# with this software.
# If not, see <https://creativecommons.org/publicdomain/zero/1.0/>.

# /etc/bash.bashrc: executed by bash(1) for interactive shells.

# System-wide bashrc file
```
 - 기본적으로 10줄 출력하지만, `-n <N>` 옵션으로 줄 수를 지정 가능
```
$ head -n2 bash.bashrc
```
```
# To the extent possible under law, the author(s) have dedicated all 
# copyright and related and neighboring rights to this software to the
```

## tail
 - 파일의 뒷부분 일부를 출력
```
$ cd /etc
$ tail bash.bashrc
```
```
  export PS1='\[\e]0;\w\a\]\n\[\e[32m\]\u@\h \[\e[35m\]$MSYSTEM\[\e[0m\] \[\e[33m\]\w\[\e[0m\]\n'"${_ps1_symbol}"' '
  ;;
esac
unset _ps1_symbol

# Uncomment to use the terminal colours set in DIR_COLORS
# eval "$(dircolors -b /etc/DIR_COLORS)"

# Fixup git-bash in non login env
shopt -q login_shell || . /etc/profile.d/git-prompt.sh
```
 - 기본적으로 10줄 출력하지만, `-n <N>` 옵션으로 줄 수를 지정 가능
```
$ tail -n2 bash.bashrc
```
```
# Fixup git-bash in non login env
shopt -q login_shell || . /etc/profile.d/git-prompt.sh
```
 - `tail -f <FILE>` : 로그 파일 업데이트 확인
    - 서버 프로세스의 로그 파일의 경우, 서버에서 요청받을 때마다 로그 파일을 업데이트하는데, 
    - `tail -f <FILE>` 실행 시, tail 프로그램이 종료되지 않고 업데이트되는 내용을 바로 출력함
    - tail 프로세스를 종료하고 셸로 돌아갈 때는 컨트롤 + C를 입력함

***
<h2 id="help">사용법과 매뉴얼</h2>

## --help
- `-help` `-h` 옵션으로 사용법 출력
- 주로 명령어의 옵션을 보는 용도로 많이 사용됨
- 도움말 출력 방법 3가지
  1. 아무런 인자 없이 명령어를 실행
  2. -h 옵션을 붙여서 실행
  3. --help 옵션을 붙여서 실행(가끔은 -help인 경우도 있음)
- `cd`의 경우에는 인자가 없으면 홈디렉터리로 이동하고 `grep`의 경우에는 인자가 없으면 기본적인 사용법을 보여줌
- 커맨드라인 세계만의 상식과 관습이 있기 때문에 프로그램마다 실행해 보는 것이 답..

## man
`man <명령어>`
 - 명령어 자체에 대한 정보를 확인
 - 리눅스, 맥

***

<h2 id="option">왜 어떤 옵션은 –를 사용하고 어떤 옵션은 ––를 사용하나요?</h2>
`-` `--`
 - 문자를 옵션으로 사용할 때는 `-`을, 문자열을 옵션으로 사용할 때는 `--`을 사용함
 - `-`에 여러 개의 옵션을 한 번에 지정할 수 있음(`-abh` == `-a -b -h`)
    - `$ ls -l -s -G -r` 명령을 `-lSGr`로 줄여서 사용할 수 있음
 - 가끔 보이는 특이한 경우로는 `<COMMAND> <OPTIONS> -- <ARGUMENT>` 형식처럼 --가 사용될 때도 있음
 - 이는 -- 앞에서 옵션 지정을 명시적으로 종료하고, 명시적으로 인자를 받는 경우에 활용됨.
 - 일반적인 규칙에 대한 문서 참고
   - [The Gnu C Library 25.1.1 Program Argument Syntax Conventions](https://www.gnu.org/software/libc/manual/html_node/Argument-Syntax.html)

***

<h2 id="escape">서바이벌 가이드: 비상 탈출 버튼 `^c`, `^d`, `^\`, `^z`</h2>
 - `^` : 컨트롤 키와 다른 키 조합을 의미
 - `^c` : <종료_interrupt> SIGINT(siginterrupt) 신호를 송출하여 실행중인 프로세스의 작업을 중단시킴 
   - (주의) 프로그램마다 신호 처리에 대한 구현이 다를 수 있음
 - `^\` : <코어덤프_core dumped> SIGQUIT 신호를 송출하여 프로세스를 종료시킨 뒤 코어를 덤프함
 - `^d` : <종료> EOF(End of File)을 의미 (입력이 완전히 종료되었음의 의미)
 - `^z` : <중지_stopped> SIGSTOP 신호를 송출하여 실행중인 작업을 중지시킴 
   - SIGCONT로 재실행 가능


***
###### 참고 사이트 및 출처 리스트
###### 1. [커맨드라인 사용법](https://www.44bits.io/ko/post/linux-and-mac-command-line-survival-guide-for-beginner#%EC%BB%A4%EB%84%90-%EC%85%B8-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%ED%84%B0%EB%AF%B8%EB%84%90-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%EC%9D%B4%EB%9E%80)
###### 2. [[OS] 커널(Kernel)이란](https://minkwon4.tistory.com/295)
###### 3. [[Linux] 리눅스 ls 명령어 사용법 & 옵션 정리 (디렉터리 목록 확인)](https://coding-factory.tistory.com/748)
###### 4. [[리눅스 / 유닉스 ] 시그널이란? 시그널(SIGNAL) 종류, 상황, 유사 시그널 차이점 ](https://jhnyang.tistory.com/143#google_vignette)