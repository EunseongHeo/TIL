# 07. Version Control

###### 강의 출처 - [2023 OSSCA 기본 교육_8-git개괄 왜git을사용하나](https://www.youtube.com/watch?v=BdgWZy87e9M&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=10), [2023 OSSCA 기본 교육_9-버전관리의중요성](https://www.youtube.com/watch?v=UVz7WCx7HEI&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=11), [2023 OSSCA 기본 교육_10-다양한버전관리시스템과커밋](https://www.youtube.com/watch?v=VVjQ6yQRFlc&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=12)

***
### 들어가며
1. <a href="#reason">버전을 관리하는 이유</a>
2. <a href="#think">버전 관리 시스템 선택 시 고려 사항</a>
3. <a href="#compare">GitHub vs GitLab vs Bitbucket</a>

***
### <span id="reason">버전을 관리하는 이유</span>

- 엔지니어가 새로운 기술을 배울 때 또는 도입하려 할 때 버전을 관리할 수 있으면,
    1. 실행 취소, 재실행(복구)이 가능함  (main reason)
    2. 버전 간 소스 코드 비교가 가능함
        - https://www.diffchecker.com/
    3. 효율적인 협업이 가능함
- 장애 발생 시 대응 시간을 줄일 수 있음

### <span id="think">버전 관리 시스템 선택 시 고려 사항</span>
- 팀의 상황
    - 팀의 구성원을 고려하여 적절한 시스템을 선택
- 설정 및 유지 관리의 용이성
    - 설정하기 쉬워야 더 빨리 사용할 수 있음
- 파일 유형 및 크기
    - 파일의 유형 및 크기가 큰 복합한 프로젝트를 처리하고 관리해야 하는 경우와
    - 단순한 디자인의 프로그램으로 작은 규모의 프로젝트를 처리하고 관리해야 하는 경우는 선택 시 다른 기준이 필요할 것이다.
    - 각 프로젝트의 특성에 따라 적절한 버전 관리 시스템을 선택하는 것이 현명할 것이다.
- 워크플로
    - 팀에서 일상적으로 사용하는 프로세스와 툴 고려
    - 버전 관리 시스템의 브랜칭 지원 여부를 고려
- 시스템 구현 타이밍
    - 프로젝트에의 영향을 줄이고 새 시스템의 도입 속도를 높이는 방향으로 버전 관리 시스템의 구현 시점을 전략적으로 결정이 필요함
- 지출 및 절감 항목
    - 기술적 배경과 관계없이 팀 전체가 쉽게 액세스할 수 있는 제품
    - 절대 팀의 효율적인 협업을 방해하지 않는 선택
    - 사용하기 어려운 버전 관리 시스템의 경우, 사용 방법에 대한 교육 및 버전 관리 베스트 프랙티스에 관한 내부 문서 작성 등에 많은 시간 비용이 발생할 수 있음
- 보안 요구 사항
    - 소스 코드, 비즈니스 문서, 절차 문서, 디자인 파일, 툴 구성 등 다른 에셋을 관리하기 위한 시스템을 선택
- 유연성 수준
    1. 로컬 버전 관리 
        - Local VCS
        - 간단히 데이터베이스를 사용해서 파일의 변경 정보를 관리하는 시스템
        - `RCS(Revision control system)`
    1. 중앙 집중식 워크플로 
        - CVCS(Centralized VCS)
        - 체크인/푸시 워크플로
        - 강력한 브랜칭 및 병합
        - `CVS`, `Subversion`, `Perforce`
    2. 분산식 워크플로
        - DVCS(Distributed VCS)
        - 메인 서버에 연결하지 않고도 원하는 시간에 체크인, 브랜칭, 병합 수행이 가능함
        - 원격 근무 가능, 느린 네트워크나 VPN에 대하여 걱정할 필요가 없음
        - `Git`, `Mecurial`, `Bazaar`, `Darcs`
    3. 멀티사이트 워크플로
        - 중앙 집중식 워크플로 + 분산식 워크플로
        - 팀원들은 일종의 소규모 형태의 중앙화된 워크플로로 작업
        - 브랜치와 진행 상황을 공유하여 팀원 간에 손쉽게 병합하고 조율 가능
        - 원하는 시간에 메인 서버에 최종적으로 푸시 가능
        - 여러 도시 또는 국가에서 코드 베이스를 공유하여 작업하는 팀에 적합

### <span id="compare">GitHub vs GitLab vs Bitbucket</span>
- 대표적인 웹 기반 Git 레포지토리 서비스 중 세 가지를 비교함
- 공통으로 제공되는 서비스
  - 버전관리 시스템
  - 코드베이스 저장소
  - 보안 기능 내장
  - 활발한 커뮤니티
- GitHub, GitLab, Bitbucket 특징
  - GitHub
      - 코드 레포지토리 호스팅 제공
      - 오픈소스 프로젝트에서 가장 선호
      - 강력한 CI/CD 파이프라인을 제공
      - 직관적인 UI와 사용 편의성, 대규모 커뮤니티
  - GitLab
      - 코드 레포지토리 호스팅 제공
      - 다른 대안보다 더 포괄적인 DevOps 도구(보안 테스트, 모니터링 등)를 제공
      - DevSecOps 팀에 추천
  - BitBucket
      - Atlassian의 오픈 데브옵스 솔루션의 기본 Git 도구
      - 코드 레포지토리로 설계되었지만, Jira 및 Confluence 통합 및 소프트웨어 프로젝트 전용
      - 광범위한 Jira 또는 Confluence 통합이 필요한 경우 추천

- 비교표
  - | Features                                | GitHub                                  | GitLab | Bitbucket                                              |
    |-----------------------------------------|-----------------------------------------|--------|--------------------------------------------------------|
    | Code repository                         | ✅                                       | ✅      | ✅                                                      |
    | Social features                         | ✅                                       |        | ❌                                                      |
    | DevOps                                  | ❓  Not as extensive  as other platforms | ✅      | ❓ Not as extensive  as other platforms                 |
    | PM tool features                        | ✅                                       | ✅      | ✅                                                      |
    | Bug/issue tracking                      | ✅                                       | ✅      | ✅                                                      |
    | AI-powered assistant                    | ✅                                       | ❌      | ❌                                                      |
    | Integrations                            | ✅ Extensive                             | ✅      | ❓ Only for Atlassian products : Jira, Confluence, etc. |
    | Advanced security                       | ✅                                       | ✅      | ✅                                                      |
    | Open-source project support (for free)  | ✅                                       | ✅      | ❌                                                      |
    | Automation features via CI/CD workflows | ✅                                       | ✅      | ✅                                                      |
    ###### 출처 - [GitHub vs GitLab vs BitBucket: Key Differences & Feature Comparison](https://marker.io/blog/github-vs-gitlab-vs-bitbucket)

###### 참고 사이트 및 출처 리스트
###### 1. (영상) [2023 OSSCA 기본 교육_8-git개괄 왜git을사용하나](https://www.youtube.com/watch?v=BdgWZy87e9M&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=10)
###### 2. (영상) [2023 OSSCA 기본 교육_9-버전관리의중요성](https://www.youtube.com/watch?v=UVz7WCx7HEI&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=11)
###### 3. (영상) [2023 OSSCA 기본 교육_10-다양한버전관리시스템과커밋](https://www.youtube.com/watch?v=VVjQ6yQRFlc&list=PL8MaVgZDhGk-z7cezrPFJ5y6v3GW_S1iF&index=12)
###### 4. (참고) [The Missing Semester of Your CS Education](https://missing-semester-kr.github.io/)
###### 5. (참고) [Diffchecker](https://www.diffchecker.com/)
###### 6. (블로그) [Unity 블로그_ 버전 관리 시스템 선택 시 고려해야 할 8가지 요소](https://blog.unity.com/kr/games/8-factors-to-consider-when-choosing-a-version-control-system)
###### 7. (블로그) [GitHub vs GitLab vs BitBucket: Key Differences & Feature Comparison](https://marker.io/blog/github-vs-gitlab-vs-bitbucket)
