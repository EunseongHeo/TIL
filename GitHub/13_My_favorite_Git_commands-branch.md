# 13. My favorite Git commands about branch

***
### 들어가며
1. <a href="#process">브랜치 생성에 대한 과정</a>
2. <a href="#i">명령어</a>
   1. <a href="#fetch">`fetch`</a>
   2. <a href="#move">브랜치 전환</a>
   3. <a href="#check">브랜치 확인</a>
   4. <a href="#d_r">브랜치 삭제 - 원격</a>
   5. <a href="#d_l">브랜치 삭제 - 로컬</a>
   6. <a href="#routine1">원격 저장소 관리 루틴</a>
   7. <a href="#routine2">팀 프로젝트 로컬 세팅 루틴</a>
   8. <a href="#routine3">작업 중 커밋이 뒤처졌을 때 루틴</a>

***
> <h2><span id="process" strong>[브랜치 생성에 대한 과정]</span></h2>
> <br/>
> 1. 코드 추가 또는 변경 부분 확인
> 
> &nbsp;&nbsp;&nbsp;[원격]
> 2. Issue 생성
> 3. 브랜치 생성 - 생성한 Issue 번호 및 추가할 코드에 대한 키워드를 활용
>   - 예시) 8-my-favorite-git-commands-branch
> 
> &nbsp;&nbsp;&nbsp;[로컬]
> 4. 필요한 명령어 수행
> 5. 로컬에서 작업
> 6. 원격으로 push
> 7. 이슈트래커 확인
> 8. PR(Pull Request)
> 
> &nbsp;&nbsp;&nbsp;[원격 및 로컬]
> 9. 브랜치 삭제

***
## <span id="i">브랜치 관련 명령어</span>
### 1. <span id="fetch">원격에서 브랜치 생성 후 로컬에 Fetch</span>
```
$ git fetch origin
```

### 2. <span id="move">브랜치로 전환</span>
```
$ git checkout <브랜치명>
$ git switch <브랜치명>
```
- 브랜치 생성 및 브랜치 전환
  - ```
    $ git checkout -b <브랜치명>
    ```

### 3. <span id="check">브랜치 확인</span>
- `-a`, `--all`: 로컬, 원격 브랜치를 모두 확인
- `-r`, `--remote`: 원격 브랜치만 확인
```
$ git branch
$ git branch -a
$ git branch -r
```

### 4. <span id="d_r">브랜치 삭제 - 원격</span>
- 예시) `$ git push origin -d 8-my-favorite-git-commands-branch`
```
$ git push <origin> -d <삭제할 브랜치 이름>
$ git push <origin> --delete <삭제할 브랜치 이름>
```

### 5. <span id="d_l">브랜치 삭제 - 로컬</span>
- 삭제 대상이 아닌 다른 브랜치로 전환 필수
```
$ git branch -d <삭제할 브랜치 이름> 
```

### 6. <span id="routine1">원격 저장소 관리 루틴</span>
- 원격 저장소 등록 
  - `$ git remote add <origin> <URL>`
- 원격 저장소 삭제
  - `$ git remote remove <origin>`
  - `$ git remote rm <origin>`
- 원격 저장소 조회
  - `$ git remote`
  - `$ git remote -v`
  - `$ git remote show <원격 저장소 이름>`
- 원격 저장소 이름 변경
  - `$ git rename <기존 이름> <변경할 이름>`

### 7. <span id="routine2">팀 프로젝트의 원격 및 로컬 세팅 루틴</span>
1. 최상위 프로젝트(upstream)를 내 원격 저장소(origin)로 가져오기
   - GitHub Organization을 통해
   - Fork를 통해
   - `$ git clone <프로젝트 URL>`
3. 원격 저장소들(upstream, origin)을 로컬에 등록하기
4. 등록 여부 확인
   - origin(fetch/push), upstream(fetch/push) <-- 4개가 조회되면 정상
```
// 2.
$ git remote add upstream <최상위 프로젝트 URL>
$ git remote add origin <내 원격 저장소 URL>

// 3.
$ git remote -v
```

### 8. <span id="routine3">작업 중 커밋이 뒤처졌을 때 루틴</span>
- `upstream`: 팀 프로젝트 또는 오픈 소스 프로젝트 (root_최상위 저장소)
- `origin`: 내 원격 저장소 (보통 내가 push 하는 저장소)
```
    ...내 커밋 rewind

$ git fetch upstream main
$ git checkout main
$ git rebase upstream/main

    ...내 커밋 올리기
    ...충돌 수정
    ...필요 시, rebase -i 활용

$ git push origin
    ...PR 생성 (origin -> upstream)
```
***
###### 참고 사이트 및 출처 리스트
###### 1. (블로그) [[효팍이의 프로그래밍] [Git]오픈소스 기여 및 협업을 위한 rebase 활용 방법, git blame 명령어로 오픈 소스 분석하기](https://ihp001.tistory.com/229)
###### 2. (블로그) [[로컬에서는 잘 되는데] Git remote 원격 저장소와 Github](https://dev-youngjun.tistory.com/46)
