# JPA 학습

## API 개발 고급 - 지연로딩과 조회 성능 최적화



### 조회용 샘플 데이터 입력

- `@PostConstruct` : `spring bean`이 다 올라오고 나면 `spring`이 호출 해 준다.



### 간단한 주문 조회 V1: 엔티티를 직접 노출

- 양방향 연관관계 문제 : 한 객체에 `JsonIgnore`로 연관관계를 끊는다.
- `Lazy Loading`하게 되면 연관관계의 대상이 되는 객체의 데이터를  `DB`에서 가져오지 않는다. 해당 객체에 `null`을 넣어 놓을 수 없으니,  `Proxy Library`에서 해당 객체를 상속받아 `proxy 객체` 즉, `ByteBuddyInterceptor`를 넣어놓는다.
- 만들어 놓은 `proxy 객체`를 사용 할 일이 있을 때, `sql`을 날려 해당 데이터를 가져온다. 이것을 `proxy 객체`를 초기화 한다고 한다.
- `Hibernate5Module`을 사용하여 `Lazy Loading`인 객체들을 `null`처리하여 가져올 수 있고 `force lazy`하여 `Lazy Loading`인 객체들을 전부 가져올 수도 있다. 하지만 이러한 방식들은 권장되는 방법이 아니다. (쿼리낭비 등)
- `Lazy Loading`을 피하기 위해 `Fetch type = Eager`으로 바꾸는 것은 `JPQL N+1` 문제나, 연관관계가 필요하지 않는 경우에도 데이터를 항상 조회해서 등 성능의 문제가 발생 할 수 있고 성능 튜닝이 매우 어려우므로 사용하지 않도록 한다.
- 성능 최적화가 필요한 경우에는 `fetch join`을 사용한다.



### 간단한 주문 조회 V2: 엔티티를 DTO로 변환

- `DTO`로 생성하여 응답한다.
- `V1`과 `V2`의 문제점? 어미어마한 쿼리의 낭비가 있다. (`N+1` 문제)
- `FetchType=LAZY`로 설정된 객체들은 `proxy 객체`로 존재하다가, 해당 데이터 호출 시 영속성 컨텍스트를 먼저 조회한다. 그리고 없다면 DB에 쿼리를 날려 조회한다.



### 간단한 주문 조회 V3: 엔티티를 DTO로 변환 - 페치 조인 최적화

- `fetch join`은 성능 최적화에 아주 많이 사용되므로 꼭 이해하도록 하자.
- `JPQL`에서 `join fetch`를 사용하여, 연관 테이블을 한번에 가져와 성능 최적화 할 수 있다.
- 장점으로는 재사용성이 높지만, 단점으로는 테이블의 불필요한 컬럼까지 다같이 조회한다.



### 간단한 주문 조회 V4: JPA에서 DTO로 바로 조회

- 기본적으로  `JPA`는 쿼리문에서 `Entity`나 `VO`만 반환 할 수 있다.
- `JPQL`을 `JdbcTemplate`처럼 필요한 컬럼만 가져와서 각각 맵핑시켜서 사용 할 수 있다. 
- 장점으로는 정말 필요한 컬럼만 가져오지만, 단점으로는 정말 해당 DTO를 위해서 만들어진 쿼리이기 때문에 재사용성이 없다.
- 성능이 좋지만 `API`에 의존적이여서 논리적 계층구조가 깨져버린다.
  - `Repository`는 `Entity`를 조회하는 용도로 사용해야 하는데 `DTO`를 조회해버린다.
  - `API` 조회용 `QueryRepository` 생성하여 관리하는 것도 하나의 방법이다.

