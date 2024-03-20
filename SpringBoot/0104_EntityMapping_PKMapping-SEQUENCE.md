# 04. Entity Mapping - 기본 키 매핑 SEQUENCE 전략
###### 인프런 - [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic)
###### 실습 GitHub Repository: hello-jpa의 커밋 번호 - [ee58488](https://github.com/EunseongHeo/hello-jpa/commit/ee58488a2fdab5d106b7a34cac83b11689940c16)

***
## 기본 키 매핑 - SEQUENCE 전략
- `@Id @GeneratedValue(strategy = GenerationType.SEQUENCE)`
- Member 클래스 코드 일부
  ```java
  import javax.persistence.*;

    @Entity
    @SequenceGenerator(
        name = "MEMBER_SEQ_GENERATOR",
        sequenceName = "MEMBER_SEQ",    //매핑할 데이터베이스 시퀀스 이름
        initialValue = 1,               //초기화 값
        allocationSize = 50             //얻어올 시퀀스 값
    )
    public class Member {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE,
        generator = "MEMBER_SEQ_GENERATOR"
    )
    private Long id;
    private String name;
  
    //...(생략)...
  }
  ```

- Main 클래스의 일부 코드
  ```java
    public Main class{
        public static void main(String[] args){
            // EntitManagerFactory 객체 생성: emf
            // EntityManger 객체 생성: em
            // EntityTransaction 객체 생성: tx
            tx.begin();
            try{
                Member member1 = new Member();
                member1.setUserName("A");

                Member member2 = new Member();
                member2.setUserName("A");

                Member member3 = new Member();
                member3.setUserName("A");

                System.out.println("=============================");
                em.persist(member1);
                em.persist(member2);
                em.persist(member3);
                System.out.println("member1.id = " + member1.getId());
                System.out.println("member2.id = " + member2.getId());
                System.out.println("member3.id = " + member3.getId());
                System.out.println("=============================");
  
                tx.commit();
            } 
            //...(생략)...
        }
    }
  ```
- JPA가 생성한 CREATE SQL
    - `create sequence MEMBER_SEQ start with 1 increment by 50`
- JPA가 생성한 SQL
    - `call next value for MEMBER_SEQ`
    - `call next value for MEMBER_SEQ`
    - ###### <a href="#console">콘솔 결과</a>에서 확인


- ### DB 시퀀스 값 - 실행 전
  - | 시퀀스(MEMBER_SEQ) |     |
    |-------------------|-----|
    | 현재 값            | -49 |
    | 증가               | 50 |

- ### DB 시퀀스 값 - 실행 후
- 첫 번째 `call next value for MEMBER_SEQ` 실행 직후의 시퀀스 값
  - | 시퀀스(MEMBER_SEQ) |    |
    |-------------------|----|
    | 현재 값            | 1  |
    | 증가               | 50 |
- 두 번째 `call next value for MEMBER_SEQ` 실행 직후의 시퀀스 값
  - | 시퀀스(MEMBER_SEQ) |    |
    |-------------------|----|
    | 현재 값            | 51 |
    | 증가               | 50 |

- ### <span id="console">콘솔 결과</span>
  ```
    [결과값]--------------------------------
    Hibernate: create sequence MEMBER_SEQ start with 1 increment by 50
    Hibernate: 
        
        create table Member (
           id bigint not null,
            name varchar(255) not null,
            primary key (id)
        )
    =============================
    Hibernate: 
        call next value for MEMBER_SEQ
    Hibernate:
        call next value for MEMBER_SEQ
    member1.id = 1
    member2.id = 2
    member3.id = 3
    =============================
    Hibernate:
        /* insert hellojpa04.Member
            */ insert
        into
            Member
            (name, id)
        values
            (?, ?)
    Hibernate:
        /* insert hellojpa04.Member
            */ insert
        into
            Member
            (name, id)
        values
            (?, ?)
    Hibernate:
        /* insert hellojpa04.Member
            */ insert
        into
            Member
            (name, id)
        values
            (?, ?)
  ```

***
## SEQUENCE 전략의 특징
> 1. `em.persist(member);` 실행
> 2. 시퀀스 지정한 값(`allocationSize` 속성값)만큼 미리 얻어오기 `call next value for MEMBER_SEQ`
>    </br><font style="color:gray;">※ 얻어온 만큼의 시퀀스 값은 JPA가 관리 ※</font>
> 3. 영속성 관리(1차 캐시에 넣기)
> 4. `tx.commit();` 시점에 DB에 SQL을 일괄 전송 <font style="color:gray;">(쓰기 지연)</font>

- 데이터베이스의 시퀀스 오브젝트를 활용한 전략
- 오라클, PostgreSQL, DB2, H2 데이터베이스 등
- PK 타입은 LONG 타입을 권장 (*String X)
- DB로부터 일정한 크기의 시퀀스를 미리 얻어와 JPA가 관리하게끔 하는 것이 전략의 가장 큰 특징임
