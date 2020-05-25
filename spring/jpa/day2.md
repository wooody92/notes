# JPA 학습

### 강의 정보

- 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발
- 김영한

## 애플리케이션 아키텍처

### 계층형 구조 사용

- controller, web : 웹 계층
- serviece : 비즈니스 로직, 트랜잭션 처리
- repository : JPA를 직접 사용하는 계층, 엔터티 매니저 사용
- domain : 엔터티가 모여 있는 계층, 모든 계층에서 사용

## 회원 도메인 개발

### 회원 리포지토리 개발

- JPQL과 SQL의 차이?
  - SQL : 테이블 대상으로 하는 쿼리
  - JPQL : 엔터티 객체를 대상으로 하는 쿼리(from의 대상이 엔터티 객체)

### 회원 서비스 개발

- `@Transactional(readOnly = true)` (읽기전용)을 사용하면 JPA가 조회하는 부분에 있어서 성능을 최적화 한다. (영속성 컨텍스트 flush 안해서 dirty checking 안하거나 하는..)

- 클래스 단에서 `@Transactional(readOnly = true)` 선언해주고, 쓰기가 필요한 메서드에서 `@Transactional` 추가해주는 것을 권장한다.

- 필드 인젝션 사용 지양 -> 세터 인젝션 사용 -> 생성자 인젝션 사용 권장한다. 서비스가 실행되면 repository가 중간에 변경되지 않는 장점이 있고, 테스트 코드 작성 시에도 이점이 있다.

  ```java
  // 필드 인젝션
  @Autowired
  private MemberRepository memberRepository;
  
  // 세터 인젝션
  private MemberRepository memberRepository;
  
  @Autowired
  public void setmemberRepository(MemberRepository memberRepository) {
    this.memberRepository = memberRepository;
  }
  
  // 생성자 인젝션
  private final MemberRepository memberRepository;
  
  @Autowired // 생략가능
  public MemberService(MemberRepository memberRepository) {
    this.memberRepository = memberRepository;
  }
  
  // lombock 활용 생성자 인젝션, final 붙은 객체만 생성자 만든다.
  @RequiredArgsConstructor
  //...//
  private final MemberRepository memberRepository
  ```

### 회원 기능 테스트

- `@Test(expected = Exception.class)`로 `try - catch` 생략 가능하다.
- `fail()`로 발생하면 안되는 부분 체크 가능하다.
- 테스트 코드 작성 시 인메모리 DB로 사용 할 수 있다.
- 테스트 코드에서는 yml 파일을 따로 가져가는 것이 괜찮다. (보고싶은 레벨이 다르기 때문)



## 상품 도메인 개발

### 상품 엔터티 개발

- 데이터를 갖고 있는 곳에서 비즈니스 로직을 처리하는 것이 응집력이 있고 객체 지향적인 설계이다.
  - Entity가 갖고 있는 stock add하거나 remove 할 때 등

### 상품 리포지토리 개발

- `EntityManager`
- `em.persist` : save & `em.merge` : update 정도로 우선 생각하자.

### 상품 서비스 개발

- 이번 경우에서는 상품 서비스는 단순히 상품 리포지토리를 위임하는 역할만 했다. 이 경우에는 컨트롤러에서 리포지토리 자체를 가져와도 무방하다.
