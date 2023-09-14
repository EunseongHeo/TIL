# 04. 깃배쉬 설치하기
###### 강의 출처
[2023 OSSCA 기본 교육_1-깃배시설치](https://www.youtube.com/watch?v=2MtgnvB4aSU&t=1037s)


***
### Git bash 설치 이유?
- 윈도우 OS 환경에서 리눅스 커맨드 사용 가능

### Git bash 다운로드 
- [https://git-scm.com/](https://git-scm.com/)

### Git bash 세팅
- 자신의 GitHub 계정에 맞춰서 최초 설정하기
- Windows환경에서 작업시 CRLF 관련 설정하기
- 명령어
    ``` 
    # 깃헙 유저네임
    $ git config --global user.name "MyName" 
  
    # 깃헙 가입시 이메일
    $ git config --global user.email myEmail@gmail.com
        
    $ git config --global core.autocrif true
    ```
### Git 최초 설정
- `git config` 도구로 설정 내용 확인 및 변경 가능
  1. `/etc/gitconfig` 파일
     - 시스템의 모든 사용자와 모든 저장소에 적용되는 설정
     - `git config --system` 옵션으로 파일의 rw 가능
     - 시스템의 관리자 권한이 필요
  2. `~/.gitconfig`, `~/.config/git/config` 파일
     - 현재 사용자(특정 사용자)에게만 적용되는 설정
     - `git config --global` 옵션으로 rw 가능
     - 특정 사용자의 모든 저장소 설정에 적용
  3. `.git/config`
     - Git 디렉토리에 있고 특정 저장소(혹은 현재 작업 중인 프로젝트)에만 적용
     - `--local` 옵션을 사용하여 이 파일을 사용하도록 지정할 수 있음
     - 기본적으로 이 옵션이 적용됨
     - 옵션 적용시 Git 저장소인 디렉터리로 이동해야 함
- `.git/config` 가 `/etc/gitconfig` 보다 우선됨

### git config 설정 확인 및 변경하기
###### 출처 - [Git Config 설정 확인 및 변경하기](https://webisfree.com/2018-07-26/git-config-%EC%84%A4%EC%A0%95-%ED%99%95%EC%9D%B8-%EB%B0%8F-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0)
    ```
    # check
    $ git config --list

    # delete
    $ git config --unset user.name
    $ git config --unset user.email

    # initialize
    $ git config --global user.name "홍길동"
    $ git config --global user.email "support@webisfree.com"
    ```

***
###### 참고 사이트 출처 리스트
###### 1. [Git, Git Bash 쉬운 설치/ Git Bash 설치 쉽고 자세한 설명/ 윈도우 OS에서 리눅스 환경 구축하기/ Git Bash란 무엇인가](https://parkjh7764.tistory.com/39)
###### 2. [Git 최초 설정](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%B5%9C%EC%B4%88-%EC%84%A4%EC%A0%95)
###### 3. [Git Config 설정 확인 및 변경하기](https://webisfree.com/2018-07-26/git-config-%EC%84%A4%EC%A0%95-%ED%99%95%EC%9D%B8-%EB%B0%8F-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0)
