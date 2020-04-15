## 오늘의 강의

### Many to One

- Category : User

  ```java
  private Long user;
  
  public void setUserId (User user) {
  	this.user = user.getId();
  }
  ```

- setter가 필요하다.

- 1:N / N:1 의 차이점?

  One to Many : 하나를 수정하면 어떤 것을 업데이트 해야 할 지 모르기 때문에 전체를 업데이트하는 쿼리를 날린다.

  Many to One : 수정 된 것 하나만 업데이트하는 쿼리를 날리지만, 이해관계가 모호해짐 (카드 : 카테고리, N : 1 보다 카테고리 : 카드, 1 : N 이 명확한 것처럼)

- DB를 수정해도 API 를 수정하면 안된다.

- DB에서 참조 키는 항상 N 인 쪽이 갖는다.

### Many to Many

- ERD는 개념적 설계이기 때문에 코드 설계와는 상관없이 요구사항을 개념적으로 설계하는 것이다.
- DB에는 외래키를 참조하는 1:N 밖에없다.
- N:M 은 1:N 을 두번 사용해서 구현할 수 있다.
