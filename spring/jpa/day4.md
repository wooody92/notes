# JPA 학습

### 강의 정보

- 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발
- 김영한

## 웹 계층 개발

### 홈 화면과 레이아웃

- `lombok - @Slf4j` 사용하면 자동으로 logger 생성해준다.
- `html` 정적 파일은 `cmd + shift + f9`로 재빌드없이 새로고침하여 변경사항 확인 할 수 있다.
- `getbootstrap.com`에서 `css, js`파일을 다운 받을 수 있다.
- `cmd + e` : 최근에 검색했던 리소스 보기

### 회원 등록 & 회원 목록 조회

- `@NotEmpty(message = "not empty error")`를 사용해서 값이 비어있으면 오류가 나게 할 수 있다.

- `@Valid`를 이용하여 `@NotEmpty`와 같은 항목을 점검 할 수 있고 만약 에러가 발생한다면 해당 로직을 끝내지 않고 `BindingResult`에 에러를 담아 로직을 진행 할 수 있다.

  ```java
  @PostMapping("/members/new")
  public String create(@Valid MemberForm form, BindingResult result) {
    if (result.hasErrors()) {
      return "members/createMemberForm";
    }
    ...
  }
  
  public class MemberForm {
    @NotEmpty(message = "회원 이름은 필수 입니다.")
    private String name;
    ...
  }
  ```

- 엔티티는 웹 계층에서 사용되는 기능을 위해(화면에 보여지는 기능을 위한) 변경되어서는 안된다. 엔티티는 핵심 비즈니스 로직만을 갖도록 순수하게 유지하고, DTO를 하나 만들도록 하자.

- 엔티티는 절대 API로 외부에 노출하지 않는다.



### 상품 등록 & 목록 & 수정

- 항목 수정 시 변경 감지를 쓰는 것이 JPA 가이드이다.
- `ModelAttribute("")`



### 변경 감지와 병합(merge)

- 하나의 영속성 컨텍스트 안에서 엔티티의 값이 바뀌면 JPA가 변경감지 후 transaction commit 시점에 알아서 바꿔준다.

- 변경감지 : dirty checking

- 준영속 엔티티

  - JPA 영속성 컨텍스트가 더 이상 관리하지 않는 엔티티
  - DB에 한번 다녀와서 기존의 식별자를(JPA가 식별할 수 있는)가지고 있는 엔티티

- 준영속 엔티티를 수정하는 2가지 방법

  - 변경 감지 기능 사용
  - 병합(merge)

- 변경감지

  ```java
  @Transactional
  public void updateItem(Long itemId, Book param) {
    // findItem은 DB에 다녀온 영속상태
    Item findItem = itemRepository.findOne(itemId);
    findItem.setPrice(param.getPrice());
    findItem.setName(param.getName());
    findItem.setStockQuantity(param.getStockQuantity());
  }
  
  /** Transaction이 끝나면 flush한다.
  /*  flush하면 JPA가 변경점을 찾는다.(dirty checking)
  /*  바뀐 값에 대해 update query를 날린다.
  */
  ```

- 병합(merge)

  - 병합은 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용하는 기능

  ```
  병합 동작 방식
  1. merge()를실행한다.
  2. 파라미터로 넘어온 준영속 엔티티의 식별자 값으로 1차 캐시에서 엔티티를 조회한다.
  2-1. 만약 1차 캐시에 엔티티가 없으면 데이터베이스에서 엔티티를 조회하고, 1차 캐시에 저장한다.
  3. 조회한 영속 엔티티( mergeMember )에 member 엔티티의 값을 채워 넣는다. (member 엔티티의 모든 값
  을 mergeMember에 밀어 넣는다. 이때 mergeMember의 “회원1”이라는 이름이 “회원명변경”으로 바
  뀐다.)
  4. 영속 상태인 mergeMember를 반환한다.
  ```

  ```
  병합시 동작 방식을 간단히 정리
  1. 준영속 엔티티의 식별자 값으로 영속 엔티티를 조회한다.
  2. 영속 엔티티의 값을 준영속 엔티티의 값으로 모두 교체한다.(병합한다.)
  3. 트랜잭션 커밋 시점에 변경 감지 기능이 동작해서 데이터베이스에 UPDATE SQL이 실행
  ```

  - 변경 감지 기능을 사용하면 원하는 속성만 선택해서 변경할 수 있지만, 병합을 사용하면 모든 속성이 변경된다. 병합시 값이 없으면 null 로 업데이트 할 위험도 있다. (병합은 기존에 존재하는 변경되지않은 필드도 포함하여, 모든 필드를 교체한다.)

  

### 상품 주문

- `Controller`는 식별자만 `Service`에 넘겨주고 `@Transactional`이 있는 하나의 영속성 안에서 비즈니스 로직이 처리 되는 것이 테스트 및 관리에 좋다.



### 추가 정리

- `@ManyToMnay`를 사용 하지 않는 이유?

  ```
  @ManyToMany 는 편리한 것 같지만, 중간 테이블( CATEGORY_ITEM )에 컬럼을 추가할 수 없고, 세밀하게 쿼
  리를 실행하기 어렵기 때문에 실무에서 사용하기에는 한계가 있다. 중간 엔티티( CategoryItem 를 만들고 @ManyToOne , @OneToMany 로 매핑해서 사용하자. 정리하면 대다대 매핑을 일대다, 다대일 매핑으로 풀어 내서 사용하자.
  ```

- 생성자의 접근제어자를 `protected`로 하는 이유?

  JPA가 객체 생성 시 리플렉션 기술을 사용할 수 있도록 지원해야 하기 때문 

  ```
  JPA 스펙상 엔티티나 임베디드 타입( @Embeddable )은 자바 기본 생성자(default constructor)를 public 또는 protected 로 설정해야 한다. public 으로 두는 것 보다는 protected 로 설정하는 것이 그나마 더 안전 하다.
  > JPA가 이런 제약을 두는 이유는 JPA 구현 라이브러리가 객체를 생성할 때 리플랙션 같은 기술을 사용할 수 있도록 지원해야 하기 때문이다.
  ```

- `FetchType = Fetch.LAZY`로 설정하는 이유?

  ```
  즉시로딩( EAGER )은 예측이 어렵고, 어떤 SQL이 실행될지 추적하기 어렵다. 특히 JPQL을 실행할 때 N+1 문제가 자주 발생한다.
  실무에서 모든 연관관계는 지연로딩( LAZY )으로 설정해야 한다.
  연관된 엔티티를 함께 DB에서 조회해야 하면, fetch join 또는 엔티티 그래프 기능을 사용한다. @XToOne(OneToOne, ManyToOne) 관계는 기본이 즉시로딩이므로 직접 지연로딩으로 설정해야 한다.
  ```

  
