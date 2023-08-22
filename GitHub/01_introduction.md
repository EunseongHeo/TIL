# 01. Introduction

## 커맨드라인 인터페이스
Command-line Interface, CLI
- Character User Interface, CUI
- 사용자가 텍스트로 명령어를 입력하고 다시 텍스트로 결과를 화면에 출력해 주는 인터페이스를 가진 컴퓨팅 인터페이스.
- [커맨드라인 사용법: 따라 하며 배우는 리눅스 명령어와 관습들](https://www.44bits.io/ko/post/linux-and-mac-command-line-survival-guide-for-beginner)
  - pwd
  - ls -al
  - cd ../..
  - 

## 터미널
Terminal, 단말기
- console, 콘솔
- 입력과 출력이 가능한 하드웨어 장비
- 가상 터미널, 터미널 에뮬레이터
- Windows Command Prompt, Windows Terminal, iTerm2, Hyper 등

## 셸
Shell, 셸
- 컴퓨터에 명령을 내리기 위한 인터페이스 역할을 하는 대표적인 CLI로 구현된 프로그램
- 기본적으로 셸은 다른 커맨드라인 프로그램들을 실행하는 용도로 사용됨
- 즉, Shell은 명령어를 통해 컴퓨터를 제어하는 방식을 의미함

## 셸과 REPL(Read-eval-print loop)
셸의 구현에 대해서 REPL이라고 함
- Read(읽기), eval(평가), print(출력) 그리고 loop(반복)
- 루비의 irb, 파이썬의 python 명령어 등 스크립트 언어들의 REPL 방식으로 구현된 인터렉티브 환경을 제공한다.
- 다양한 셸 종류 [ Bash 셸](https://www.gnu.org/software/bash/bash.html), [Zsh](https://www.zsh.org/), * [Oh My Zsh 설정 프레임워크](https://github.com/ohmyzsh/ohmyzsh)

## 셸과 SSH의 차이
SSH란? 

- Secure Shell Protocl
- 인터넷과 같은 공용 네트워크를 통해 사로 통신할 때 보안 측면에서 안전하게 통신하기 위해 사용하는 프로토콜
- 즉, SSH는 명령어 방식으로 컴퓨터를 원격에서 제어하는 방식이라고 할 수 있음
- 이러한 원격 제어 통신의 보안을 위해 SSH는 Public Key와 private Key라는 한 쌍의 key를 이용해 인증함



(SSH Server를 서비스로 등록한 리눅스 서버로 예시)

ID/Password 또는 SSH 키를 발급하여 인터넷이나 내부망으로 연결된 다른 컴퓨터에서 서버 컴퓨터로 접속하는 것이 가능하다.
 - 이 때, 접속하는 방법은 아래와 같다.
    1. 가상 터미널 어플리케이션에서 ssh 명령어로 서버 컴퓨터에 접속한다.
    2. 외부 컴퓨터에서 전용 SSH 클라이언트를 사용하여 서버 컴퓨터에 접속한다.
 1. 가상 터미널로 로컬 머신에서 셸을 실행하는 경우,
   - tty 장치가 할당됨
   - 이 때는 터미널 앱 자체가 tty라고 할 수 있음
 2. ssh로 원격 장치에 접속할 경우,
   - 원격 장치에 pty(pseudo tty)가 생성됨
   - 즉, 의사 터미널 장치인 pty 장치는 shell과 같은 역할을 수행한다고 이해할 수 있음
   - 그리고, 원격 장치의 입력을 전달 하거나 실행된 결과(pty에 출력되는 내용)를 SSH 클라이언트로 전달할 때 SSH를 통하여 동작하는 것으로 이해할 수 있음

 - 셸과 SSH의 역할을 나눠서 생각해보면 이해에 도움됨




***
###### 출처 - [커맨드라인 인터페이스, 셸, 터미널이란?](https://www.44bits.io/ko/keyword/command-line-interface-cli-shell-and-terminal)