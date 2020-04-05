## 오늘의 강의

### SQL Join

- 부모 테이블의 테이블 명을 컬럼이름으로 외래 키를 지정 할 수 있다.

- ```
  user u left outer join github g on u.id = g.user
  ```

- 생성자로 따로 안만들고 내부 객체하나 만들어 사용하기

- ```
  public void setGithub(Github github) { this.github = gigthub;}
  ```

- 1:1 관계에서 굳이 테이블을 두개로 나누어 조인을 해야할까?

- Null이 생기는 단점은 있지만 하나의 테이블로 하는 것이 성능상 유리할수 있다.

- 객체는 어떻게 해야할까? 테이블에 합치기 또는 @Embedded  태그 사용할 수 있다.

- 1:Many 관계에서는 Set, Map 그리고 List를 활용하여 사용 할 수 있다.


#### 강의 자료
- https://lucas.codesquad.kr/course/마스터즈-프로젝트/학습자료-BE/Join-and-Index
- 호눅스 유튜브 강의
