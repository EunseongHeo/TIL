# 03. Command Line (2)

### 들어가며
08. <a href="#move">라인 앞뒤로 이동하기</a>
09. <a href="#history">내가 입력했던 명령어 찾기</a>
10. <a href="#string">문자열: 큰따옴표와 작은따옴표의 차이</a>
11. <a href="#multiLine">멀티라인 명령어 실행하기</a>
12. <a href="#tab">탭으로 자동 완성</a>
13. <a href="#hiddenFile">숨김 파일</a>
14. <a href="#linux">리눅스 콘솔 단축키</a>

***
<h2 id="move">라인 앞뒤로 이동하기</h2>
- `Home`, `^a`: 명령어의 맨 앞으로 이동
- `End`, `^e`:  명령어의 맨 뒤로 이동
- `alt + ←`, `alt + f`: 단어 단위로 왼쪽 이동 
- `alt + →`, `alt + b`: 단어 단위로 오른쪽 이동

***
<h2 id="history">내가 입력했던 명령어 찾기</h2>
- `↑`: 이전 명령어
- `history`: 최근에 입력한 명령어 조회
  - `$ history <N>`: 최근에 입력한 <N> 개의 명령어 조회
  - `$ history !<N>`: <N> 번호의 명령어 조회
- `^r`: 최근에 입력한 명령어 조회
  - `^r <char/string>`: <char> 문자/ <string> 문자열(가)이 들어간 명령어 조회

***
<h2 id="string">문자열: 큰따옴표와 작은따옴표의 차이</h2>
- 따옴표 없이 사용하는 경우 일반적으로 빈칸이 인자를 구분하는 용도로 사용됨
  - 따옴표로 감싸서 명시적으로 문자열임을 알릴 수 있음 (큰따옴표/작은따옴표)
    - 큰따옴표: 배시 셸의 문법에 따라 특수한 입력값들이 자동으로 치환됨
      ```
      # 환경 변수 출력
        $ echo "Hello, $USER."
        Hello, 44bits.
      ---------------------------
      # 환경 변수 비 출력
        $ echo "\"Hello, \$USER.\""
        "Hello, $USER."
      ---------------------------
      # \n, \t 적용하려면 echo 명령어에 -e 옵션 추가
      ```
      ```
      # "" 안에서 ! 사용 시 문제 발생
        bash-3.2$ echo -e "Hello, world!"
        bash: !": event not found
      ---------------------------
      # set +H 명령: 히스토리 관련 치환 기능 비활성화
        bash-3.2$ set +H
        bash-3.2$ echo -e "Hello, world!"
        Hello, world!
      ```
    - 작은따옴표: 치환 없이 입력한 그대로 내용을 전달
      ```
        $ echo 'Hello, world.'
        Hello, world.
        $ echo 'Hello, $USER.'
        Hello, $USER.
      ---------------------------
      # 작은따옴표 문자열에서 작은따옴표를 쓰는 일반적인 방법은 없음
      # ANSI-C 방식은 가능
        $ echo $'Hello, \'$USER\''
        Hello, '$USER'
      ```

***
<h2 id="multiLine">멀티라인 명령어 실행하기</h2>
- 셸에서는 \ 문자로 여러 줄에 걸쳐 명령어를 실행할 수 있음
- 단, \ 뒤에 스페이스가 들어가지 않도록 주의(이스케이프로 해석될 수 있음)
- ```
    $ docker run -d \
       -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
       -e MYSQL_DATABASE=wp \
       -e MYSQL_USER=wp \
       -e MYSQL_PASSWORD=wp \
       --name mysql \
       --network=app-network \
       mysql:5.7
  ```
- 멀티라인 명령어를 셸에서 바로 입력하는 대신 에디터를 사용하면 좀 더 편리함
- 셸에서 `^x`, `^e`를 연속해서 입력하면 $EDITOR 환경변수에 지정된 에디터가 바로 실행되는데 편집한 내용을 저장하면 셸에서 바로 실행할 수 있음
- VS Code를 사용하고자 하는 경우 EDITOR 변수에 code -w를 지정
  - ```
    $ export EDITOR='code -w'
    $ ^x ^e
    ```
  - `Command + S`: 저장
  - `Command + W`: 에디터 종료
  - 참고 - [셸에서 멀티라인 명령어 편집하고 실행하기](https://www.44bits.io/ko/post/editing-multiline-command-on-shell)

***
<h2 id="tab">탭으로 자동 완성</h2>
- `tab`: 자동 완성
  - `Display all ___ possibilities? (y or n)`: y 누르면 ___로 시작하는 프로그램 목록으로 보여줄게
  - `space`: 다음 페이지로
  - ```
    $ cat <TAB>
    airport     nacyot.txt
    ```
  - ```
    $ cat n<TAB>
    $ cat nacyot.txt
    ```
- 셸 설정 등에 따라서 더 다양하고 강력한 자동완성 기능을 사용할 수 있음

***
<h2 id="hiddenFile">숨김 파일</h2>
- `.`으로 시작하는 파일: 숨김 파일(dotfiles)
- `$ ls -a`: 숨김 파일을 포함한 모든 파일의 목록을 보여주는 명령어
    - `.`으로 시작하는 파일은 보통 설정 파일을 저장하는 용도
    - 자동으로 생성되기도 하고 설정을 위해 사용자가 작성하기도 함

***
<h2 id="linux">리눅스 콘솔 단축키</h2>
###### 출처 - [[엠칩의 일기장] 리눅스 콘솔 단축키 및 명령어](https://4475.tistory.com/489)
### 터미널 실행 관련 단축키
- `Ctrl + Alt + T`: 터미널 실행
- `Ctrl + Shift + T`: 터미널 내에서 새로운 탭으로 터미널 실행
- `Ctrl + Shift + N`: 터미널 내에서 새로운 창으로 터미널 실행
- `Ctrl + Shift + W`: 탭으로 실행된 터미널 종료
- `Ctrl + Shift + Q`: 현재 터미널 종료
- `Ctrl + Shift + F`: 터미널 내에서 문자열 검색

### 터미널 내에서의 단축키
- `Shift + Ctrl + c`: 복사하기
- `Shift + Ctrl + v`: 붙여넣기
- `Ctrl + l`: 화면 Clear
- `Alt + F1 ~ F12`: 콘솔 이동
- `Alt + (← / →)`: 이전/다음 콘솔로 이동
- `Ctrl + Scroll Lock`: 프로세스 목록보기
- `Shift + Scroll Lock`: 메모리 상태 정보보기

#### 셸 상에서 실행 중인 프로그램을 제어하는 단축키
- `Ctrl + c`: 실행 중인 프로그램 중지
- `Ctrl + z`: 실행 중인 프로그램 일시 정지
- `%`: 일시 정지된 프로그램 다시 실행

#### bash 상에서 기본 입력 모드인 emacs 스타일인 경우
- `Tab`: 자동완성
- `Ctrl + d`: 로그아웃
- `Ctrl + r`: 히스토리 찾기
- `Ctrl + s`: 키보드 잠금
- `Ctrl + q`: 잠긴 키보드 풀기
- `Ctrl + m`: Enter
- `Ctrl + p`: 이전 명령어 (Up)
- `Ctrl + n`: 다음 명령어 (Down)
- `Ctrl + l`: 화면 지우기 (clear)
- `Ctrl + y`: 버퍼의 내용 붙여넣기
- `Ctrl + a`: 입력 라인의 처음으로 이동 (Home)
- `Ctrl + e`: 입력 라인의 끝으로 이동 (End)
- `Ctrl + b`: 커서를 왼쪽으로 이동(Left)
- `Ctrl + f`: 커서를 오른쪽으로 이동 (Right)
- `Ctrl + xx`: 커서를 이전 위치로 이동
- `Ctrl + u`: 커서 왼쪽의 문자들을 버퍼에 저장 후 삭제
- `Ctrl + k`: 커서 오른쪽의 문자들을 버퍼에 저장 후 삭제
- `Alt + l`: 커서 위치에서 문자열 끝까지 소문자로 변환
- `Alt + u`: 커서 위치에서 문자열 끝까지 대문자로 변환
- `Alt + t`: 두 단어 위치 바꾸기
- `Alt + b`: 커서를 다음 단어로 이동
- `Alt + f`: 커서를 이전 단어로 이동

***
###### 참고 사이트 출처 리스트
###### 1. (블로그) [[44BITS] 커맨드라인 사용법](https://www.44bits.io/ko/post/linux-and-mac-command-line-survival-guide-for-beginner#%EC%BB%A4%EB%84%90-%EC%85%B8-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%ED%84%B0%EB%AF%B8%EB%84%90-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%EC%9D%B4%EB%9E%80)
###### 2. (참고) [[gun.org] Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html#Shell-Parameter-Expansion)
###### 3. (블로그) [[엠칩의 일기장] 리눅스 콘솔 단축키 및 명령어](https://4475.tistory.com/489)
