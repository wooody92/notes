# JPA 학습

### 강의 정보

- 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발
- 김영한

## 주문 도메인 개발

### 주문, 주문 상품 엔티티, 리포지토리 개발

- 생성 메서드, 비즈니스 로직, 조회 로직 모두 엔티티 클래스 내부에 작성 할 수 있다.
- 엔티티 생성의 경우 생성자는 `protected` 접근제어자 혹은 `@NoArgsConstructor(access = AccessLevel.PROTECTED)`로 막고 따로 `create` 메서드를 만들어 관리하는 것이 유지보수에 더 좋다.

### 주문 서비스 개발

- `cascade = CascadeType.ALL`의 경우 참조하는 주인이 private Owner인 경우에만 사용해야 한다. `order - orderItems`와 같이 다른 테이블과 참조되지 않고 연관관계의 주인과 독립적으로 의존적 일 때 사용해야 한다. (`orderItems`는 `order`에서만 참조 된다.) 
  - Persist 하는 life cycle이 동일해서 사용해도 무방하다.
- 여기저기서 참조하는 중요한 테이블이라면 사용하면 안된다. 무분별하게 사용하면 예상치 못하게 데이터가 업데이트 되거나, 삭제 될 수 있다.
- `JPA`를 사용 시 엔티티 안에서 데이터만 바꾸면 DB를 직접 건드는 `JdbcTemplate`이나 `MyBatis`와는 다르게,  `dirty checking` 즉, 변경된 항목만 감지하여(변경 내역 감지) 자동으로 업데이트 쿼리를 날린다.
- 엔티티에 핵심 로직을 몰아넣는 스타일을 `도메인 모델 패턴`이라고 한다. 서비스 계층은 단순히 엔티티에 필요한 요청을 위임하는 역할을 한다. (좀 더 객체지향스럽다.)
- 반대로 엔티티에는 비즈니스 로직이 거의 없고 서비스 계층에서 대부분의 비즈니스 로직을 처리하는 것을 `트랜잭션 스크립트 패턴`이라고 한다. (주로 `sql`을 다룰 때 사용했던 패턴)
- 어느 것을 사용하던 정답은 없다. 현재 문맥에 맞는 패턴을 사용하면 된다.

### 주문 검색 기능 개발

- 페이징 처리 관련 경우는 아래와 같이 처리할 수 있다.

  ```java
  em.createQuery("JPQL")
    .setParameter("name", orderSearch.getMemberName())
    .setFirstResult(100) // 100번부터 시작하여 조회
    .setMaxResults(1000) // 최대 1000개까지의 결과 조회
    .getResultList()
  ```

- JPA에서 동적쿼리를 어떻게 해결해야 하는가? `MyBatis`는 동적 쿼리 생성이 편하다는 장점이 있다.

- 방법 1. `JPQL로 처리` 직접 동적 쿼리 로직 작성한다. 코드 자체 양이 많아 지저분하고, 실수로 인한 버그 발생 확률 높다. (권장하지 않는다.)

- 방법 2. `JPA Criteria` : JPQL을 자바 코드로 사용 할 수 있도록 도와주는 것이다. JPA에서 표준으로 제공하는 방식이나 복잡하다. 유지보수 측면에서 좋지않다.  (권장하지 않는다.)

- 방법 3. `Querydsl` 처리 (권장하는 방식이다.)

  ```java
  public List<Order> findAll(OrderSearch orderSearch) {
    
    QOrder order = QOrder.order;
    QMember member = QMember.member;
    
    return query
      .select(order)
      .from(order)
      .join(order.member, member)
      .where(statusEq(orderSearch.getOrderStatus()),
            nameLike(orderSearch.getMemberName()))
      .limit(1000)
      .fetch();
  }
  ```
