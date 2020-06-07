## AIRBNB

- https://github.com/codesquad-member-2020/airbnb-02



### Study Keyword

- [x] Spring Data JPA
- [x] Stream map
- [x] Stream filter
- [ ] Spring Web MVC & Servlet
- [ ] Static Factory Method 학습
- [ ] @PropertySource (https://kingbbode.tistory.com/39)
- [ ] Double Linked List
- [ ] @EntityScan
- [ ] Flyway
- [x] @Embedded, @Embeddable
- [x] @Enumerated(EnumType.STRING)
- [x] @DateTimeFormat(pattern = "yyyy-MM-dd")
- [x] @Transactional
- [x] Fetch Type(Lazy, Eagal)
- [x] orphanRemoval
- [x] @ElementCollection
- [x] @CollectionTable



### ERD

<img width="980" alt="스크린샷 2020-06-05 오후 6 17 20" src="https://user-images.githubusercontent.com/58318041/83974147-0078f580-a926-11ea-914b-0aeb46c429a2.png">



### PR Review

- 1주차

  https://github.com/codesquad-member-2020/airbnb-02/pull/33

- 2주차

  https://github.com/codesquad-member-2020/airbnb-02/pull/99

- 3주차

  https://github.com/codesquad-member-2020/airbnb-02/pulls



-----

### Daily Log

#### 0518 (월)

- 호눅스 강의
- 기획서 분석
- Mock API 작성

#### 0519 (화)

- 도메인 분석
- DB 구조 설계
- ERD 작성
- Mock API 문서 부분 작성

#### 0520 (수)

- Spring Data JPA Hibernate 사용 논의
- 개발환경 설정
- Docker - MySQL 설치
- Mock.csv 파일 data 입력

#### 0521 (목)

- 인원, 날짜, 가격범위 데이터 요청양식 논의
- Spring Data JPA - MySQL schema 연결
- DB 데이터 컨트롤러 사용하여 출력 (Entity, DTO, Repository 설정)
- @OneToMany, @ManyToOne 사용하여 1:N 관계 연결

#### 0522 (금)

- DTO 생성
- `JsonIgnore`, `@ToString(exclude = "")` 무한 순환 참조 에러 해결
- `TestCode` 작성
- `EC2` - `RDS` 에 `CSV file` 입력
- 배포

#### 0525 (월)

- PR review 및 refactoring
- `flyway` 적용
- `@Embedded` 사용하여 `Room` -` Locale` 클래스 분리
- `OAuth` 기능 추가
- `query parameter` 추가
- `location` 정보로 숙소 리스트 필터 기능

#### 0526 (화)

- `EnumType.STRING` 변경
- `price_min`, `price_max` query parameter 가격 필터링 기능 추가
- `checkin`, `checkout` query parameter 예약 가능 날짜 필터링 기능 추가
- `location` 미입력 시 전체 출력되도록 수정

#### 0527 (수)

- JWT 생성 기능 추가
- iOS custom url scheme에 맞춰 OAuth redirect 변경
- 예약하기 기능

#### 0528 (목)

- 페어 PR review 진행 (즐겨찾기 기능)
- `Entity cascade` 책임에 대한 논의
- `Entity - Value Object`에 대한 논의
- 예약취소 기능

#### 0529 (금)

- 분업 진행한 브랜치 merge conflict 해결
- PR 및 질문사항 작성
- 배포

#### 0601 (월)

- 2주차 PR review
- 호눅스 수업 - 쿼리 성능 개선하기
- `Room - User : ManyToMany`로 변경
- 숙소 상세보기 API 구현
- 숙소 예약, 취소 시 유저정보 반영하도록 기능 추가

#### 0602 (화)

- 사용자의 즐겨찾기 리스트 API 구현
- JWT 인터셉터 구현
- JWT 검증 후 Decoding 기능 구현

#### 0603 (수)

- Image Entity -> VO 변경
- JPA 학습
- Github Action 학습

#### 0604 (목)

- `JWT` 기반 정보 활용하도록 리팩토링
- 로그인 하지 않고 접속 시 `guest` 유저로 접속하도록 추가
- `OAuth` 로그인 시 `DB`에 유저정보 없으면 추가
- 변경사항 포스트맨 업데이트
- 배포

------

### 아쉬운 점

- 다음 프로젝트에는 Query DSL 사용해보기
- Github Action 해보기

### 피드백

