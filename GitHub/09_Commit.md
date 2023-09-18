# 09. Commit
###### 강의 출처 - [2023 OSSCA 기본 교육_10-다양한버전관리시스템과커밋](https://www.youtube.com/watch?v=VVjQ6yQRFlc&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=12), [2023 OSSCA 기본 교육_12-커밋퀴즈](https://www.youtube.com/watch?v=99poozGCBIE&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=14), [2023 OSSCA 기본 교육_13-커밋체크아웃](https://www.youtube.com/watch?v=YpRTrVvjdvw), [2023 OSSCA 기본 교육_14-커밋체크아웃 퀴즈](https://www.youtube.com/watch?v=pQPCWWdLbw0), [2023 OSSCA 기본 교육_15-detachedHEAD와시나리오별 해결 방법](https://www.youtube.com/watch?v=eJ65CP6cJhI), [2023 OSSCA 기본 교육_19-커밋생성 커밋메시지컨벤션](https://www.youtube.com/watch?v=2fSt4oiLWKE&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=21)

***
### 들어가며
1. <a href="#commit">Commit 이란?</a>
2. <a href="#often">얼마나 자주 커밋을 만들어야 하는가?</a>
3. <a href="#msg">Commit Message</a>
4. <a href="#checkout">Commit Checkout</a>
5. <a href="#detached">Detached HEAD</a>
5. <a href="#stash">Stash</a>
- <a href="#instruction">명령어</a>

***
## <span id="commit">Commit 이란?</span>
- Git의 기본 단위
- 커밋마다 설명이 담긴 message가 있음
> The git commit command captures a snapshot of the project's currently staged changes.
###### 출처 - [Bitbucket Tutorials_ Git commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit)

***
## <span id="often">얼마나 자주 커밋을 만들어야 하는가?</span>
> One commit per logical change
- 단, team by team, company by company
- 단, 커밋 크기, PR의 크기 고려 필요
- Quiz
- | 변경 내용                                     | 작음 | 적당함 | 큼 |
  |-------------------------------------------|------|--------|----|
  | 약 일주일 정도 걸려 구현한  새로운 기능을 담은 커밋            |      |        | ✅  |
  | README파일에 3개의 오타를 발견했는데, 그중 하나를 고치고 만든 커밋 | ✅    |        |    |
  | 한 시간 정도 들여 구현한 새로운 기능을 담은 커밋              |      | ✅      |    |
  | 두 개의 함수에서 각각 버그를 발견하여 한꺼번에 고친 후 만든 커밋     |      |        | ✅  |
  - 마지막 변경 내용의 경우, 1개 함수 버그 수정 후 commit 생성이 원칙임
  - ###### 논리적 변경이 있을 때 commit 하는 것이 원칙

***
## <span id="msg">Commit Message</span>
 ```
 $ git commit -m "commit message"
 $ git commit --message "commit message"
 $ git commit
 ```
  - 좋은 커밋 메시지란?
    1. 제목과 본문을 한 줄 띄워 분리하기
    2. 제목은 영문 기준 50자 이내로
    3. 제목 첫 글자를 대문자로
    4. 제목 끝에 `.` 금지
    5. 제목은 `명령조`로
    6. 본문은 영문 기준 72자마다 줄 바꾸기
    7. 본문은 `어떻게`보다 `무엇을`, `왜`에 맞춰 작성하기
    ###### 출처 - [좋은 커밋 메시지를 작성하기 위한 7가지 약속](https://meetup.nhncloud.com/posts/106)
  - 단, 회사마다 다르고 팀마다 다를 수 있다.

***
## <span id="checkout">Commit Checkout</span>
### Checkout
  - 점검, 검사

### Commit Checkout 을 하는 이유?
  - 커밋 체크아웃해서 특정 시점의 코드 상태 살펴보기 위해
  - 어느 시점에 버그가 있는 코드가 추가되었는지 추적하기 위해
  - 롤백 프로세스 관련 스크립트를 작성 할 때 
  - 등등

*** 
## <span id="detached">Detached HEAD</span>
### HEAD ?
  - 현재 체크아웃한 브랜치의 가장 최신 커밋(마지막)을 가리키는 포인터
  - 일반적으로 HEAD는 브랜치 이름을 가리킴
  - 특정 커밋으로 체크아웃한 경우, HEAD는 detached head 상태로 변경됨

### Detached HEAD 상태
- `$ git checkout [커밋ID]`
- 해당 상태에서 커밋하는 경우, 기존의 커밋과 다른 특수한 커밋이 생성되므로 주의가 필요함

### Reflog
- Detached HEAD 상태에서 생성한 커밋 이력 확인할 수 있음
- `$ git reflog` : HEAD가 가리켰던 커밋들의 이력을 조회하는 명령어
    - 시나리오
    : 실수로 Detached HEAD 상태에서 commit을 생성했다. 이 커밋에 대하여 코드를 복구하려고 하는데 해당 Commit ID를 모른다. 어떻게 해야 할까?
    
    ```
        $ git reflog 
        $ git checkout [커밋ID]
    ```
  - 참고 문서 - [Git - git-reflog Documentation](https://git-scm.com/docs/git-reflog)

***
## <span id="stash">Stash</span>
- (안전한 곳에) 넣어 두다[숨기다]
- `$ git stash`: 스택에 임시저장
- `$ git stash pop`: 임시 저장된 내용을 복구
  - 단, 붙여 넣을 곳으로 checkout 한 후 실행 주의 

***
### <sapn id="instruction">명령어</span>
- 조회
  - `$ git log`: 로그 조회 (터미널)
  - `$ gitk`: 로그 조회 (Git GUI)
  - `$ git reflog`: 참조 로그 조회
  - `$ git status`: 상태 조회
- Commit 생성
  - `$ git commit -m "commit message"`
  - `$ git commit --message "commit message"`
  - `$ git commit`
- `--help` 옵션
  - `$ git log --help`
- Checkout
  - `$ git checkout [커밋ID]`: *Detached HEAD
- Stash
  - `$ git stash`: 임시저장
  - `$ git stash pop`: 임시 저장된 내용 복구
  - 단, 스택에 저장됨

***
###### 참고 사이트 및 출처 리스트
###### 1. (영상) [2023 OSSCA 기본 교육_10-다양한버전관리시스템과커밋](https://www.youtube.com/watch?v=VVjQ6yQRFlc&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=12)
###### 2. (영상) [2023 OSSCA 기본 교육_12-커밋퀴즈](https://www.youtube.com/watch?v=99poozGCBIE&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=14)
###### 3. (영상) [2023 OSSCA 기본 교육_13-커밋체크아웃](https://www.youtube.com/watch?v=YpRTrVvjdvw)
###### 4. (영상) [2023 OSSCA 기본 교육_14-커밋체크아웃 퀴즈](https://www.youtube.com/watch?v=pQPCWWdLbw0)
###### 5. (영상) [2023 OSSCA 기본 교육_15-detachedHEAD와시나리오별 해결 방법](https://www.youtube.com/watch?v=eJ65CP6cJhI)
###### 6. (영상) [2023 OSSCA 기본 교육_19-커밋생성 커밋메시지컨벤션](https://www.youtube.com/watch?v=2fSt4oiLWKE&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=21)
###### 7. (참고) [Visualizing Git](https://git-school.github.io/visualizing-git/)
###### 8. (문서) [Git - git-reflog Documentation](https://git-scm.com/docs/git-reflog)
