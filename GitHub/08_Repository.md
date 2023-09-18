# 08. Repository
###### 강의 출처 - [2023 OSSCA 기본 교육_11-저장소클론받고로그살펴보기](https://www.youtube.com/watch?v=tIPYV-T7s50&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=12&t=1095s&pp=iAQB), [2023 OSSCA 기본 교육_16-저장소의 정체](https://www.youtube.com/watch?v=Yj9sOR1D7mI&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=18), [2023 OSSCA 기본 교육_17-TIL 저장소와 마크다운 문법](https://www.youtube.com/watch?v=5K8d66nChRs&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=18)

***
### 들어가며
1. <a href="#repo">Repository</a>
2. <a href="#clone">Clone</a>
3. <a href="#log">Log</a>
- <a href="#instruction">명령어</a>

***
## <span id="repo">Repository</span>
- 리포/레파지토리/저장소
- 여러 파일을 하나로 모은 컬렉션
- `.git` 디렉터리가 있는 디렉터리를 의미함
- 모노리포, 멀티리포
  - 모노리포 : 시스템의 각 모듈을 하나의 리포지토리에서 관리하는 방법
  - 멀티리포 : 시스템의 각 모듈을 개별 리포지토리에서 관리하는 방법
    ###### 참고 - [[Buzzvil Tech] 멀티리포 vs 모노리포](https://tech.buzzvil.com/handbook/multirepo-vs-monorepo/)
    ###### 참고 - [[Medium] Dev: MonoRepo 개념과 장단점 알아보기](https://medium.com/hcleedev/dev-monorepo-%EA%B0%9C%EB%85%90-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-33fd3ce2b767)
- `$ git init`: 저장소 초기화

***
## <span id="clone">Clone</span>
- `$ git clone [Address]`
- 저장소 복제하기
  - `clone` 받을 때 `.git` 디렉터리도 함께 다운받아짐.
- `clone`은 분산 버전 관리 시스템의 특징 중 하나임
  - 장애 발생 경우 감소

***
## <span id="log">Log</span>
- 에러 로그, 깃 로그, 서버에 남은 로그
  - `$ git log`

***
### <sapn id="instruction">명령어</span>
- 저장소
    - `$ git init`: 저장소 초기화
    - `$ mkdir [Directory 이름]`: 디렉터리 생성
    - `$ rm -rf .git`: 저장소 삭제
      ###### (-: 옵션, r: 하위에 있는 것들도 재귀적으로 제거, f: 경고를 무시고 강제로 지우겠다는 의미)
- `$ git clone [Address]`: 주소의 저장소를 복제하기
- `$ git log`: 로그 조회

***
###### 참고 사이트 및 출처 리스트
###### 1. (영상) [2023 OSSCA 기본 교육_11-저장소클론받고로그살펴보기](https://www.youtube.com/watch?v=tIPYV-T7s50&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=12&t=1095s&pp=iAQB)
###### 2. (영상) [2023 OSSCA 기본 교육_16-저장소의 정체](https://www.youtube.com/watch?v=Yj9sOR1D7mI&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=18)
###### 3. (영상) [2023 OSSCA 기본 교육_17-TIL 저장소와 마크다운 문법](https://www.youtube.com/watch?v=5K8d66nChRs&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=18)
###### 4. (참고) [[Medium] Dev: MonoRepo 개념과 장단점 알아보기](https://medium.com/hcleedev/dev-monorepo-%EA%B0%9C%EB%85%90-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-33fd3ce2b767)
###### 5. (참고) [[Buzzvil Tech] 멀티리포 vs 모노리포](https://tech.buzzvil.com/handbook/multirepo-vs-monorepo/)
###### 6. (GitHub) [마크다운 markdown 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601)
###### 7. (블로그) [MarkDown 사용법 총정리](https://heropy.blog/2017/09/30/markdown/)
###### 8. (참고) [Table Generator](https://www.tablesgenerator.com/markdown_tables)
