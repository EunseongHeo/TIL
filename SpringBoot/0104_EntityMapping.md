# 04. Entity Mapping
###### 인프런 - [자바 ORM 표준 JPA 프로그래밍 - 기본편](https://www.inflearn.com/course/ORM-JPA-Basic)
###### 실습 GitHub Repository - [hello-jpa](https://github.com/EunseongHeo/hello-jpa)
###### 이슈#6 - [Entity Mapping 실습](https://github.com/EunseongHeo/hello-jpa/issues/6)

***
### 들어가며
1. 객체와 테이블 매핑
    - 엔티티 매핑 소개
    - 객체와 테이블 매핑
      - @Entity
      - @Table
2. DB 스키마 자동 생성
   - DDL 생성 기능
   - 속성
   - DDL 생성 기능
3. 필드와 컬럼 매핑
   - 매핑 어노테이션
   - @Column
   - @Temporal
   - @Enumerated
   - @Lob
   - @Transient
4. 기본 키 매핑
   - 직접 할당
   - 자동 생성
     - IDENTITY 전략
     - SEQUENCE 전략
     - TABLE 전략
     - AUTO 전략
   - 권장하는 식별자 전략
***
## 1. 객체와 테이블 매핑
### 1.1. 엔티티 매핑 소개
- 객체와 테이블 매핑	-	@Entity, @Table
- 필드와 컬럼 매핑	-	@Column
- 기본 키 매핑		-	@Id
- 연관관계 매핑		-	@ManyToOne,@JoinColum

### 1.2. 객체와 테이블 매핑
#### 1.2.1. @Entity
- JPA가 관리하는 엔티티임을 명시
- 기본 생성자 필수
- final 클래스, enum, interface, inner 클래스에서 사용 제한
- 속성: name
    - 기본값: 클래스 이름
    - 가급적 기본값 사용 권장
#### 1.2.2. @Table
- 엔티티와 매핑할 테이블 지정
- 속성 표
- | 속성 			| 기능	 				| 기본값	    |
  |-----------------------|---------------------------------------|-------------------|
  | name 			| 매핑할 테이블 이름 			| 엔티티 이름을 사용|
  | catalog 		| 데이터베이스 catalog 매핑     	|		    |
  | schema 		| 데이터베이스 schema 매핑		|		    |
  | uniqueConstraints(DDL)| DDL 생성 시에 유니크 제약 조건 생성   |		    |

***
## 2. DB 스키마 자동 생성
### 2.1. DDL 생성 기능
- 객체 중심 개발을 위함
- DDL을 애플리케이션 실행 시점에 자동 생성
- 운영 장비에서의 사용을 권장하지 않음
### 2.2. 속성
- `persistence.xml'
- `hibernate.hbm2ddl.auto`
    - `property name="hibernate.hbm2ddl.auto" value="create"`
    - `property name="hibernate.hbm2ddl.auto" value="create-drop"`
    - `property name="hibernate.hbm2ddl.auto" value="update"`
    - `property name="hibernate.hbm2ddl.auto" value="validate"`
    - `property name="hibernate.hbm2ddl.auto" value="none"` // 안 씀
    - 옵션 정리표
    - | 옵션		| 설명							                            |
      |---------------|--------------------------------------|
      | create	| 기존 테이블 삭제 후 다시 생성 (DROP + CREATE) 		 |
      | create-drop 	| create와 같으나 종료 시점에 테이블 DROP (테스트용)	  |
      | update 	| 변경분만 반영(운영 DB에는 사용하면 안 됨)		          |
      | validate 	| 엔티티와 테이블이 정상 매핑되었는지만 확인		            |
      | none 		| 사용하지 않음						                        |
        - 운영 장비에서는 validate 또는 none을 사용 권장 (create/create-drop/update X)
        - 개발 초기 단계에서는 create 또는 update 권장
        - 테스트 서버에서는 update 또는 validate 권장
### 2.3. DDL 생성 기능
- run time에 영향을 주지 않지만 어노테이션 또는 어노테이션의 속성 지정을 통해 적절한 DDL을 자동으로 생성하는 기능
- 제약 조건, 유니크 제약 조건 추가 등
    - @Column(nullable = false, length = 10)
    - @Table(uniqueConstraints = {@UniqueConstraint( name = "NAME_AGE_UNIQUE",  columnNames = {"NAME", "AGE"} )})
###### ※ DDL 생성 기능은 DDL 자동 생성 시에만 사용되고 JPA 실행 로직에는 영향을 주지 않음 ※



***
## 3. 필드와 컬럼 매핑
- 매핑 어노테이션
    - @Column - 	컬럼 매핑
    - @Temporal - 	날짜 타입 매핑
    - @Enumerated - 	enum 타입 매핑
    - @Lob -		BLOB, CLOB 매핑
    - @Transient - 	특정 필드를 컬럼에 매핑하지 않음(매핑 무시)
### 3.1. @Column
- `@Column(name = "name", insertable = false, updatable = false, nullable = false, unique = true) `
- 속성 정리표
- | 속성 			 | 설명 									| 기본값						|
  |------------------------|------------------------------------------------------------------------------|-------------------------------------------------------|
  | name 			 | 필드와 매핑할 테이블의 컬럼 이름 						| 객체의 필드 이름					|
  | insertable 		 | 등록 가능 여부  								| TRUE							|
  | updatable		 | 변경 가능 여부								| TRUE							|
  | nullable(DDL) 	 | null 값의 허용 여부								| 							|
  | unique(DDL) 		 | 한 컬럼에 간단한 유니크 제약조건 생성 시 사용 `@Column(unique = true)`	| 							|
  | columnDefinition (DDL) | 데이터베이스 종속적인 옵션 지정	 					| 필드의 자바 타입 인식 및 해당 DB의 적절한 컬럼 타입   |
  | length(DDL) 		 | 문자 길이 제약조건 (String 타입만)	 					| 255							|
  | precision(DDL)	 | 소수점을 포함한 전체 자릿수 (BigDecimal/BigInteger 타입)			| precision=19 						|
  | scale(DDL) 		 | 소수의 자릿수  (BigDecimal/BigInteger 타입)					| scale=2						|
    - 보통 `@Column`의 `unique` 속성보다 `@Table`의  `uniqueConstraints` 속성을 더 많이 사용함 _(유니크 제약 조건의 이름을 지정할 수 있기 때문)
        - ###### @Table(uniqueConstraints = "uniqueTest")
    - `columnDefinition` 속성의 예시
        - ###### @Column(columnDeﬁnition = "varchar(100) default 'EMPTY'")
    - `precision`, `scale` 속성은  참고로 double, ﬂoat 타입에는 적용되지 않는다.
### 3.2. @Temporal
- 날짜 타입 매핑 시 사용 `java.util.Date`, `java.util.Calendar`
- 사실, `LocalDate`, `LocalDateTime`을 사용할 때는 생략 가능 (최신 하이버네이트 지원)
- 속성: value
    - `TemporalType.DATE`: 날짜, 데이터베이스 date 타입과 매핑  `2013–10–11`
    - `TemporalType.TIME`: 시간, 데이터베이스 time 타입과 매핑  `11:11:11`
    - TemporalType.TIMESTAMP: 날짜와 시간, 데이터베이스 timestamp 타입과 매핑  `2013–10–11 11:11:11`
### 3.3. @Enumerated
- 자바 enum 타입을 매핑 시 사용
- 주의! EnumType.STRING 사용 권장
- 속성: value
    - 기본값: `EnumType.ORDINAL`
    - EnumType.ORDINAL: enum 순서를 데이터베이스에 저장
    - EnumType.STRING: enum 이름(값)을 데이터베이스에 저장
### 3.4. @Lob
- 데이터베이스 BLOB, CLOB 타입과 매핑
- @Lob에는 지정 가능한 속성이 없음
- 매핑하는 필드 타입이 문자면 CLOB 매핑, 나머지는 BLOB 매핑
    - CLOB: String, char[], java.sql.CLOB
    - BLOB: byte[], java.sql.BLOB
### 3.5. @Transient
- 해당 필드를 매핑하지 않음
- 데이터베이스에 저장 및 조회가 되지 않음
- 주로 메모리상에서만 임시로 어떤 값을 보관하고 싶을 때 사용

***
## 4. 기본 키 매핑
### 4.1. 직접 할당
- @Id 어노테이션만 사용
- 실행 시 PK 값을 할당해 주어야 함
### 4.2. 자동 생성
- `@Id @GeneratedValue(strategy = GenerationType.<TYPE명>)`
    - `IDENTITY`: 데이터베이스에 위임함, MYSQL
    - `SEQUENCE`: 데이터베이스 시퀀스 오브젝트 사용, ORACLE
    - `TABLE`: 키 생성용 테이블 사용, 모든 DB에서 사용
    - `AUTO`: 방언에 따라 자동 지정, 기본값
> #### 4.2.1. IDENTITY 전략
> - `@Id @GeneratedValue(strategy = GenerationType.IDENTITY)` - 필드에 지정
> - 기본 키 생성을 데이터베이스에 위임함
> > 1. PK 값 = null
> > 2. `em.persistence(객체);` 실행 시 INSERT 쿼리 실행
> > 3. DB가 PK 값에 적절한 값을 자동으로 입력
> >  	- 테이블 생성 쿼리를 보면, `generated by generated by default as identity`를 확인할 수 있음
> 4. DB에서 입력한 PK 값을 JPA 조회하여 1차 캐시에 저장
> - MySQL, PostgreSQL, SQL Server, DB2 데이터베이스 등
> - 단점이라면 `em.persist()` 실행 시 쓰기 지연 기능이 동작하지 못한다는 것이 있음

> #### 4.2.2. SEQUENCE 전략
> - `@Id @GeneratedValue(strategy = GenerationType.SEQUENCE)` - 필드에 지정
> - 데이터베이스 시퀀스는 유일한 값을 순서대로 생성하는 특별한 데이터베이스 오브젝트
> > 1. `em.persist(member);` 실행
> > 2. 시퀀스 지정한 값(`allocationSize` 속성값)만큼 미리 얻어오기 `call next value for MEMBER_SEQ`
> > 3. 영속성 관리(1차 캐시에 넣기)
> > 4. `tx.commit();` 시점에 DB에 SQL을 일괄 전송
> > - 오라클, PostgreSQL, DB2, H2 데이터베이스 등
> - PK 타입은 LONG 타입을 권장 (*String 타입 X)
- `@SequenceGenerator` 사용 시, `@GeneratedValue` 어노테이션 속성 `generator = <sequenceGenerator 이름>` 지정 권장
- `@SequenceGenerator` - 클래스에 지정
- `@SequenceGenerator` 속성 정리표
- | 속성			| 설명 							                    | 기본값		|
  |-----------------------|-------------------------------|-----------------------|
  | name 			| 식별자 생성기 이름 					              | 필수			|
  | sequenceName 		| 데이터베이스에 등록된 시퀀스 이름 		         | hibernate_sequence	|
  | initialValue 		| 시퀀스 DDL을 생성할 때 처음 시작하는 수 지정		 | 1			|
  | allocationSize 	| 시퀀스 한 번 호출에 증가하는 수			         | 50			|
  | catalog		| 데이터베이스의 catalog 이름				        |			|
  | schema		| 데이터베이스의 schema 이름				         |			|
- ###### initialValue 속성은 DDL 생성 시에만 사용됨
> #### 4.2.3. TABLE 전략
> - `@Id @GeneratedValue(strategy = GenerationType.TABLE)` - 필드에 지정
> - 키 생성 전용 테이블을 하나 만들어서 데이터베이스 시퀀스를 흉내 내는 전략
> - 장점: 모든 데이터베이스에 적용 가능
> - 단점: 성능(락, 최적화 등) 이슈
- `@TableGenerator` 사용 시, `@GeneratedValue` 어노테이션 속성 `generator = <tableGenerator 이름>` 지정 권장
- `@TableGenerator` - 클래스에 지정
- `@TableGenerator` 속성 정리표
- | 속성 				| 설명 							                       | 기본값		|
  |-------------------------------|----------------------------------|-----------------------|
  | name 				| 식별자 생성기 이름 					                 | 필수			|
  | table				| 키 생성 테이블명 					                  | hibernate_sequences	|
  | pkColumnName 			| 시퀀스 컬럼명 					                    | sequence_name		|
  | valueColumnName		| 시퀀스 값 컬럼명 					                  | next_val 		|
  | pkColumnValue 		| 키로 사용할 값 이름 					                | 엔티티 이름		|
  | initialValue 			| 초깃값, 마지막으로 생성된 값이 기준이다. 		       | 0			|
  | allocationSize 		| 시퀀스 한 번 호출에 증가하는 수(성능 최적화에 사용됨)	 | 50			|
  | catalog, schema 		| 데이터베이스 catalog, schema 이름			     | 			|
  | uniqueConstraints(DDL)	| 유니크 제약 조건 지정 가능				              | 			|
#### 4.2.4. AUTO 전략
> - `@Id @GeneratedValue(strategy = GenerationType.AUTO)` - 필드에 지정
> - JPA가 적절한 전략을 선택
> - `@SequenceGenerator` 또는 `@TableGenerator`를 알맞게 지정하여 사용

### 4.3. 권장하는 식별자 전략
- 기본 키 제약 조건: null 아님, 유일, 변하면 않음
- `변하면 않음` - 즉, 5년 이상 변하지 않는 키
  - 미래까지 이 조건을 만족하는 자연 키는 찾기 어려움
  - 대리키(대체키_비즈니스와 상관없는 키)를 사용 권장
- 권장: Long 형 + 대체키 + 키 생성 전략 사용
- 권장: AUTO 전략 또는 SEQUENCE 전략
