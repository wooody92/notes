# JPA 학습

## 프로젝트 환경설정

### 강의 정보

- 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발
- 김영한

### 프로젝트

- JPA란? 강력한 JAVA ORM 표준
- 도메인 모델 설계 - 엔티티 설계 - 테이블 설계 - JPA ORM으로 맵핑 - 애플리케이션 아키텍처 구성 - 핵심 비즈니스 로직 개발

### JPA와 DB 설정, 동작확인

- yml 사용방법

- `@Transactional`이 Test case에 있으면 작업 후 DB를 롤백한다.

- 롤백을 원치않는다면 `@Rollback(false)` 사용하여 커밋할 수 있다.

- 하나의 트랜잭션에서 같은 영속성 컨텍스트에서 식별자가 같으면 같다고 인식한다. (1차 캐시에서 있는 값 사용) 

- 실제 쿼리문에 어떤 파라미터가 입력되는 지 확인하고 싶을 때 아래 항목 추가한다.

  ```
  logging:
    level:
      org.hibernate.SQL: debug
      org.hibernate.type: trace
  ```

### 

## 도메인 분석 설계

### 연관관계 매핑 분석

- 일대다, 다대일 양방향 관계에서는 외래키가 있는(1:N에서 N 부분) 엔터티를 주인으로 정하는 것이 좋다. 연관관계의 주인쪽의 값을 세팅해야 값이 변경된다.(외래 키가 있는 곳이 연관관계의 주인으로 하는 것이 정석. 관리 및 유지보수 측면에서 편하다.)
- 일대다에서 일 부분에 있는 `mappedBy`는 단순히 읽기만 하는 역할(즉, 단순 조회용)이며, 연관관계의 주인쪽에 세팅을 해야 값이 변경된다.
- 외래키가 가까운 곳에 있는 것을 연관관계의 주인으로 정하는 것이 좋다.
- 다대다 관계에서는 `@ManyToMany` 사용은 권장되지 않고 1:N + N:1로 풀어내는 것이 권장된다.

### 엔터티 클래스 개발

- Enum Type 사용 시 `@Enumerated(EnumType.STRING)`을 사용하여 Enum 중간에 값이 들어와도 순서가 밀리지 않도록 방지한다. `@Enumerated(EnumType.ORDINAL)`을 사용하면 순서에 따라 숫자로 맵핑되는데 순서가 중간에 추가되거나 달라지면 장애 문제가 발생한다.
- 실무에서 `getter`는 실용적인 관점에서 많이 사용하여 열어 놓기도 하지만, `setter`의 경우는 열어놓지 않고 필요한 경우 비즈니스 메서드를 만드는 것이 추후 유지보수 측면에서 훨신 좋다.
- `setter`를 제거하고, 생성자에서 값을 모두 초기화해서 변경 불가능한 클래스로 만들도록 하자. 자바에서 리플렉션 같은 기술이 필요한 비어있는 기본 생성자는 `protected`로 설정하자.
- 테이블의 아이디는 `@Column(name = "table_id")`로 설정하는 것이 f.k와 일치성도 있고, DB관리 입장에서 편하다.

### 엔터티 설계시 주의점

- Entity에서는 가급적 Setter를 사용하지 말자. 변경포인트가 많아서 유지보수가 어렵다.

- **모든 연관관계는 지연로딩으로(lazy loading) 설정한다.**

  - 즉시로딩(Eager)은 예측이 어렵고, 어떤 SQL이 실행될지 추적하기 어렵다. 특히 JPQL을 실행할 때 N+1 문제가 자주 발생한다.

  - 연관된 에터티를 함께 DB에서 조회해야 하면, fetch join 또는 엔터티 그래프 기능을 사용한다.

  - @XToOne(OneToOne, ManyToOne) 관계는 기본이 `EAGER`(즉시로딩)이므로 지연로딩으로 설정해야 한다.

  - 연관관계에서 Lazy Loading 하지 않으면, N+1 문제가 발생 할 수 있다.

  - 아래와 같은 상황에서 1개의 order 조회 시 연관관계인 100개의(N개) member가 같이 조회 될 수 있다. (order가 100개라면 100* 100(N) 쿼리가 요청됨)

    ```java
    publlic class Order {
    	@ManeyToOne(fetch = FetchType.EAGER)
      @JoinColumn(name = "member_id")
      private Member member;
    }
    ```

  - 그렇다면 order에서 member를 한번에 가져오고 싶다면? `fetch join` 또는 `엔터티 그래프` 기능을 사용한다.

- 컬렉션은 필드 레벨에서 초기화 하는 것이 안전하다.

  ```java
  @OneToMany(mappedBy = "member")
  private List<Order> orders = new ArrayList<>();
  ```

  - `null`문제에서 안전하다.
  - `Hibernate`는 엔터티를 영속화 할 때, 컬렉션을 감싸서 `Hibernate`가 제공하는 내장 컬렉션으로 변경된다. 임의의 메서드에서 잘못 생성하면 `Hibernate` 내부 메커니즘에 문제가 발생 할 수 있다.

- `cascade = CascadeType.ALL` 연관된 컬럼을 한번에 관리한다. 저장, 삭제 시 동시에 업데이트 된다.

  - 아래의 경우 order 변경 시 연관되어있는 orderItems도 전부 업데이트 된다.

    ```java
    publlic class Order {
    @OneToMany(mappedBy = 
    "order", cascade = CascadeType.ALL)
      private List<OrderItem> orderItems = new ArrayList<>();
    }
    ```

- 연관관계 편의 메서드는 연관관계의 주인이 되는 쪽에 있으면 편하다.

  

### 학습 키워드

- `@PersistenceCopntext` : EntityManage
- `@Inheritance(strategy = InheritanceType.SINGLE_TABLE)`
- `@DiscriminatorColumn(name = "dtype")`, `@DiscriminatorValue("")`

