## BASEBALL

- https://github.com/codesquad-member-2020/baseball-08

### TODO

- [x] 기획서 및 도메인 분석
- [x] DB 구조 설계
- [ ] M:N 테이블 설계
- [x] JdbcTemplate으로 CRUD DAO 구현
- [x] Mock API
- [x] AWS 인프라 구축 (VPC 네트워크 상 EC2-RDS 연결)
- [x] DTO 작성
- [ ] JdbcTemplate 별도의 @Configuration 클래스로 선언하여 스프링 빈으로 준비하기



### Study Keyword

- [x] @Builder (DAO에 활용)
- [ ] Stream (DTO 생성자 활용)
- [x] Aggregation
- [x] RestTemplate
- [x] HttpEntity
- [x] @Transactional (shared lock vs. exclusive lock)
- [x] HttpHeaders
- [x] JdbcTemplate.query vs. JdbcTemplate queryForObject
- [ ] Spring Web MVC & Servlet
- [ ] Static Factory Method 학습
- [ ] @PropertySource (https://kingbbode.tistory.com/39)
- [ ] Double Linked List
- [x] SQL group by
- [x] SQL group_concat
- [x] SQL distinct
- [x] SQL join
- [x] SQL coalesce



-----

### Daily Log

#### 0504 (월)

- 그라운드 룰 설정
- 기획서 및 도메인 분석
- DB 구조 설계

#### 0505 (화)

- DB 구조 설계
- ERD 작성
- 테이블 및 엔터티 작성

#### 0506 (수)

- 팀, 선수 데이터 입력
- 테이블 수정
- Mock API 및 문서 작성

#### 0507 (목)

- AWS 인프라 구축
- VPC 설정
- EC2 - RDS 연결
- 우아한 CRUD 세미나 시청
- JdbcTemplate 이용 CRUD 연습

#### 0508 (금)

- DAO 구조 논의
- Entity, DTO, DAO 책임에 대한 논의 
- OAuth 기능 추가

#### 0511 (월)

- 호눅스 DB Index 강의
- Entity, DTO, DAO 책임에 대한 학습
- SQL group_concat 학습
- SQL distinct 학습
- Join Query 사용하여 DTO, DAO 작성

#### 0512 (화)

- SQL coalesce 학습
- SQL group by 학습
- 테스트를 위한 이니셜 데이터 추가 입력
- 테이블 변경 (히스토리 로그 및 필요한 컬럼 추가)
- Join Query 사용하여 DTO, DAO 작성

#### 0513 (수)

- Branch merge 및 Conflict 해결
- 게임 진행 화면 API DAO 구현
- DTO, DAO 마무리 및 리팩토링
- 팀 선택 API 구현
- 게임 선택 API 구현
- 야구 로직 작성

#### 0514 (목)

- EC2-RDS 사용하여 배포
- OAuth 정상동작 확인
- 팀 선택 시 선택가능하면 자동 선택되도록 로직 변경
- 야구게임 로직 구현
- Branch merge 및 Conflict 해결
- 배포 후 MySQL 및 테스트에서 발생하는 버그 수정
- History 로그 기능 추가

#### 0514 (금)

- 배포 후 멀티 유저 테스트
- 각종 버그 수정 
- 데모



### 아쉬운 점

- Many To Many 테이블 구조를를 사용해보지 않았다.
- 프로젝트를 할 때 마다 DB 설계의 중요성을 느낀다. 잘하고 싶은데 어떻게 해야 잘하는 걸까
- 너무 지쳐서 스스로 만족스러운 코드도 아니고, 리팩토링도 하지 않았다.



### 피드백

- 1주차

- 회고

  - 이번 프로젝트에서는 개인의 생상선보다 페어와 팀으로 함께 개발하는 것에 포커스를 맞추어 진행했습니다.
    - 간단한 변수 네이밍부터 컨벤션, 설계까지 전부 서로 합의 후 진행했습니다.
    - 개발단계에서 각자의 방식에 대해 설명하고 무엇이 더 올바른 방법일까 서로 의견을 가감없이 공유했습니다.
    - 몰랐던 부분에 대해서는 빠르게 배울 수 있었고, 알았던 부분에 대해서는 다른 방식의 접근법에 대해 배웠습니다.
  - 개인 사정으로 컨디션 관리를 잘 못해서, 프로젝트에 집중을 많이 못했습니다. 다음주에는 좀 더 자기관리를 잘 해야겠다고 생각했습니다.

  <img width="1315" alt="스크린샷 2020-05-17 오후 8 23 03" src="https://user-images.githubusercontent.com/58318041/82143107-594ff380-987c-11ea-8ad5-730f61c09128.png">

- 2주차

  <img width="1315" alt="스크린샷 2020-05-17 오후 8 22 23" src="https://user-images.githubusercontent.com/58318041/82143122-6ff64a80-987c-11ea-8332-5e62177314f8.png">



-----

## 프로젝트 생각들

### 1. Entity, DTO, DAO에 대한 생각

### 질문

1. DB 데이터를 DAO를 이용하여 Entity vs. DTO 어디에 연결 시키는 게 맞을까?
2. 하나의 요청에 하나의 쿼리를 날리고, JOIN을 사용하기 위해서는 불필요한 데이터를 거를 필요가 있다.
3. Entity에 연결하면 불필요한 전체 데이터까지 불러와야 하는 단점이 있다.
4. DTO에 연결하면 하나의 요청에 하나의 쿼리만 날릴 수 있지만, DTO에 DAO를 연결시켜도 되는걸까?

### 답변

1. DAO는 Entity와 연결되는게 맞다. 그러나, 위와 같은 이유로 실제로는 DTO를 이용하여 조회하기도 한다.
2. 단순쿼리 여러개 vs. Join을 이용한 복잡한 쿼리 한개 -> 정말 복잡한 관계가 아니라면, 보통은 후자가 괜찮다.
3. DTO를 만드는 시점? DAO vs. Service -> 더 깔끔한 곳에서 생성

### 결론

- 이번 프로젝트에서는 DTO에 DAO를 연결하여 진행해 보았다.
- 처음에는 쿼리수를 줄이고, 불필요한 데이터조회를 하지않아 더 효율적이고 좋을 것이라고 생각했다.
- 하나의 DTO는 DAO를 이용하여 하나의 쿼리만 요청한다 라는 것이 목표였다.
- 프로젝트를 진행하다보니 응답해줘야 하는 데이터들이 복잡하게 얽혀있고 테이블 구조 설계를 잘못하면 쿼리문 작성이 엄청 복잡해졌다.
- 생산성이나 유지보수 측면에서 오히려 독이 될 수 있을것 같다고 생각했다.
- 덕분에 sql문법은 많이 배웠지만, 다음부터는 Entity - DAO를 사용하는 것으로 하자.



### 2. Aggregation에 대한 생각

- Aggregate의 범위는 어디까지일까? 삭제 시 같이 삭제되어도 되는 범위로 생각하면 괜찮다.
- Aggregation root를 생각해보면, 선수 정보를 담고있는 team과 게임 정보를 담고있는 game으로 생각 해 보았다.
- 그렇다면, history(이닝 log)의 경우 game aggregation에 붙는 게 더 어울려 보인다.
- 그러면 각 두개의 루트의 dao와 join을 사용하여 구현 해보는 것이 어떠할까
