# 04. Entity Mapping - 기본 키 매핑 TABLE 전략
###### 인프런 - [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic)
###### 실습 GitHub Repository: hello-jpa의 커밋 번호 - [1c70196](https://github.com/EunseongHeo/hello-jpa/commit/1c701969164fda6dcfd0ec717dedd309914b536f)

***
## 기본 키 매핑 - TABLE 전략
- `@Id @GeneratedValue(strategy = GenerationType.TABLE)`
- Member 클래스 코드 일부
  ```java
  import javax.persistence.*;

    @Entity
    @TableGenerator(
        name = "MEMBER_SEQ_GENERATOR",  //식별자 생성기 이름    (필수)
        table = "MY_SEQUENCES",         //키 생성 테이블명      (기본값: hibernate_sequences)
        pkColumnValue = "MEMBER_SEQ",   //키로 사용할 값 이름   (기본값: 엔티티 이름)
        allocationSize = 50  //한 번 호출에 증가시킬 수 _시퀀스   (기본값: 50)
    )
    public class Member {

    @Id
    @GeneratedValue(strategy = GenerationType.TABLE,
        generator = "MEMBER_SEQ_GENERATOR"
    )
    private Long id;
    private String name;
  
    //...(생략)...
  }
  ```

- Main 클래스의 일부 코드
  ```java
    import javax.persistence.*;
    import javax.persistence.Persistence;
  
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
- JPA가 생성한 CREATE TABLE SQL
  ```h2
  create table MY_SEQUENCES (
    sequence_name varchar(255) not null,
    next_val bigint,
    primary key (sequence_name)
  )
  ```
- JPA가 생성한 SQL
    - SELECT
      ```h2
      select
        tbl.next_val
      from
        MY_SEQUENCES tbl
      where
        tbl.sequence_name=? for update
      ```
    - UPDATE
      ```h2
       update
          MY_SEQUENCES
      set
          next_val=?  
      where
          next_val=?
          and sequence_name=?
      ```
    - ###### <a href="#console">콘솔 결과</a>에서 확인

- ### MY_SEQUENCES 테이블 조회 결과 - 실행 후
    - | MY_SEQUENCES | NEXT_VAL |
      |--------------|----------|
      | MEMBER_SEQ   | 100      |


- ### <span id="console">콘솔 결과</span>
  ```
    [결과값]--------------------------------
    Hibernate: 
        
        create table Member (
           id bigint not null,
            name varchar(255) not null,
            primary key (id)
        )
    Hibernate: 
    
       create table MY_SEQUENCES (
          sequence_name varchar(255) not null,
           next_val bigint,
           primary key (sequence_name)
       )
    Hibernate: insert into MY_SEQUENCES(sequence_name, next_val) values ('MEMBER_SEQ',0)
    =============================
    Hibernate:
        select
            tbl.next_val
        from
            MY_SEQUENCES tbl
        where
            tbl.sequence_name=? for update
    
    Hibernate:
        update
            MY_SEQUENCES
        set
            next_val=?  
        where
            next_val=?
            and sequence_name=?
    Hibernate:
        select
            tbl.next_val
        from
            MY_SEQUENCES tbl
        where
            tbl.sequence_name=? for update
    
    Hibernate:
        update
            MY_SEQUENCES
        set
            next_val=?  
        where
            next_val=?
            and sequence_name=?
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
> 2. @TableGenerator에서 지정한 값(`allocationSize` 속성값)만큼 미리 UPDATE SQL 실행 
  </br>&nbsp;&nbsp;<font style="color:gray;">※ SELECT SQL로 다음 값이 있는지 조회한 후 적절하게 UPDATE SQL 실행 ※</font>
  </br>&nbsp;&nbsp;<font style="color:gray;">※ 얻어온 만큼의 시퀀스 값은 JPA가 관리 ※</font>
> 3. 영속성 관리(1차 캐시에 PK 값 넣기)
> 4. `tx.commit();` 시점에 DB에 SQL을 일괄 전송 <font style="color:gray;">(쓰기 지연)</font>

- 키 생성 전용 테이블을 생성하여 데이터베이스 시퀀스 오브젝트를 흉내 내는 전략
  - 장점: 모든 데이터베이스에 적용 가능
  - 단점: 성능(락, 최적화 등) 이슈
