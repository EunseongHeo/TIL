# 11. Branch
###### 강의 출처 -[2023 OSSCA 기본 교육_20-브랜치와브랜치생성 간단한이슈트래커실습](https://wwwyoutubecom/watch?v=F5wd17ll9Cc&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=22), [2023 OSSCA 기본 교육_21-브랜치병합 자동머지메커니즘](https://wwwyoutubecom/watch?v=F7BU4fC8nxU&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=22), [2023 OSSCA 기본 교육_22-브랜치자동병합 충돌 실습](https://wwwyoutubecom/watch?v=9R6xe-dH28Y&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=23), [2023 OSSCA 기본 교육_23-브랜치충돌해결실습](https://wwwyoutubecom/watch?v=MHHrreJGWW8&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=24), [2023 OSSCA 기본 교육_24-리베이스](https://wwwyoutubecom/watch?v=InXwX9BeKVU&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=25), [2023 OSSCA 기본 교육_25-개인학습방법 마무리](https://wwwyoutubecom/watch?v=CVVpCwK3-oQ&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=26)

***
### 들어가며
1. <a href="#work">브랜치 생성과 이슈트래커</a>
    - <a href="#branch">브랜치</a>
    - <a href="#seq">브랜치 생성 순서</a>
2. <a href="#merge">Merge</a>
    - <a href="#autoMerge">브랜치 병합 자동 머지 메커니즘</a>
    - <a href="#pr">Pull Request</a>
    - <a href="#conflict">브랜치 병합 충돌</a>
3. <a href="#rebase">Rebase</a>
    - <a href="#differences">`merge`와 `rebase`의 차이</a>
    - <a href="#benefit">`rebase` 사용 시 이점</a>
- <a href="#instruction">명령어</a>

***
## <span id="work">브랜치 생성과 이슈트래커</span>

### <span id="branch">브랜치</span>
    나무 : tree
    가지 : branch
    줄기(기둥) : trunk

- Branch 정의
    > A branch in Git is simply a lightweight movable pointer to one of these commits.
         
    ###### 출처 - [[git] Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell#:~:text=A%20branch%20in%20Git%20is,branch%20pointer%20moves%20forward%20automatically.)
  
    > Git branches are effectively a pointer to a snapshot of your changes.

    ###### 출처 - [[Bitbucket] Git Branch](https://www.atlassian.com/git/tutorials/using-branches)
  - ###### Git의 HEAD는 브랜치를 가리키고, 브랜치는 커밋을 가리키는 구조로 되어있다고 이해할 수 있음
- 브랜치는 어떤 `특정한 목표`를 가지고 코드를 수정하기 시작할 때 생성함

### <sapn id="seq">브랜치 생성 순서</span>
1. 이슈를 생성한다. 
   - issue-tracker
2. 이슈에 맞는 브랜치를 생성한다.
   - 이슈에 맞게 브랜치 명명
   - 이슈 번호와 이슈 내용에 관련하여 명명하면 직관적으로 업무를 이해할 수 있음
     - (예시) 1-modifyMyInfoProfilePreview
3. 생성한 브랜치로 전환하여 작업한다.
```
$ git branch [브랜치명]
$ git checkout [브랜치명]
------------------------
$ git checkout -b [브랜치명]
```
```
# 동일
$ git checkout [브랜치명]
$ git switch [브랜치명]
```

***
## <span id="merge">Merge</span>
- 두 브랜치를 합칠 때 쓰는 명령어
- 일반적(3-way merge시)으로 머지 커밋이 생성됨

### <span id="autoMerge">브랜치 병합 자동 머지 메커니즘</span>
    조건)
    A브랜치를 B브랜치에 합칠 때
    1. B브랜치로 체크아웃함
       (스위치하여 해당 브랜치로 전환)
    2. $ git merge A

### <span id="pr">Pull Request</span>
- 두 브랜치를 합칠 때 쓰는 방법이나 `코드 리뷰` 과정을 거치게 됨
- 최종 merge 버튼 클릭에 대한 과정은 팀마다, 회사마다 다를 수 있음

### <span id="conflict">브랜치 병합 충돌</span>
- 두 브랜치를 병합할 때 같은 부분에 대하여 다른 내용으로 충돌이 일어날 수 있는데, 이를 해결하는 것은 개발자의 의지로 수행되어야 함
> 순서
> 1. 두 브랜치 병합을 진행한다.
> 2. 충돌이 일어난다.
> 3. 충돌된 부분에 대한 코드를 정리한다.
> 4. 필요 없는 코드에 대하여 삭제한다.
> 5. 다시 병합을 진행한다.

***
## <span id="rebase">Rebase</span>
- base를 새로 세팅하다 (옮겨간다).
- 주둔지를 옮긴다.
###### interactive rebase에 대해서는 다음 파일에서 다룸

### <sapn id="differences">`merge`와 `rebase`의 차이</span>
- 일반 `merge`는 대부분의 경우에 `merge commit`이 생성됨 (fast-foward 의 경우 제외)
- `rebase`는 'merge commit'이 생성되지 않음
    ###### Git Branch 전략 참고 -  [우아한 형제들 Git-flow](https://techblog.woowahan.com/2553/)

### <span id="benefit">`rebase` 사용 시 이점</span>
- 머지 커밋이 생성되지 않으므로 커밋 그래프가 단순해짐
- 리베이스 후에는  커밋 ID가 변경됨
- 단, 협업 시 주의

***
### <sapn id="instruction">명령어</span>
- Branch
  - `$ git branch [브랜치명]`
  - `$ git checkout [브랜치명]`
  - `$ git switch [브랜치명]`
  - `$ git checkout -b [브랜치명]`
- 리눅스
  - `$ mkdir [디렉터리명] && cd [디렉터리명]/`: *&&
- Merge
  - `$ git merge [브랜치명]`
- Rebase
  - `$ git rebase [브랜치명]`

***
###### 참고 사이트 및 출처 리스트
###### 1. (영상) [2023 OSSCA 기본 교육_20-브랜치와브랜치생성 간단한이슈트래커실습](https://www.youtube.com/watch?v=F5wd17ll9Cc&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=22)
###### 2. (영상) [2023 OSSCA 기본 교육_21-브랜치병합 자동머지메커니즘](https://www.youtube.com/watch?v=F7BU4fC8nxU&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=22)
###### 3. (영상) [2023 OSSCA 기본 교육_22-브랜치자동병합 충돌 실습](https://www.youtube.com/watch?v=9R6xe-dH28Y&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=23)
###### 4. (영상) [2023 OSSCA 기본 교육_23-브랜치충돌해결실습](https://www.youtube.com/watch?v=MHHrreJGWW8&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=24)
###### 5. (영상) [2023 OSSCA 기본 교육_24-리베이스](https://www.youtube.com/watch?v=InXwX9BeKVU&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=25)
###### 6. (영상) [2023 OSSCA 기본 교육_25-개인학습방법 마무리](https://www.youtube.com/watch?v=CVVpCwK3-oQ&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=26)
###### 7. (참고) [[우아한 형제들] 우린 Git-flow를 사용하고 있어요](https://techblog.woowahan.com/2553/)
###### 8. (참고) [learn git branching](https://learngitbranching.js.org/?locale=ko)
