## SIDEDISH

- https://github.com/codesquad-member-2020/sidedish-11

### TODO

- [x] 테이블 설계
- [x] DTO Wrapper 추가
- [ ] MySQL 연결 테스트
- [ ] ERD 작성
- [ ] 각 카테고리 항목 별 데이터 출력해보기
- [ ] 전체 디테일 아이템 출력해보기
- [ ] JDBC Template 이용 DAO 학습 및 구현
- [ ] OAuth 학습 및 구현
- [ ] 주문 품절 관련 기능
- [ ] git과 bash, crontab을 이용해서 자동 배포스크립트를 작성
- [ ] tomcat 사용 배포



### Study Keyword

- [ ] @Builder
- [ ] Aggregation
- [ ] RestTemplate
- [ ] @Transactional
- [x] DTO, DAO
- [ ] JDBC Template
- [ ] OAuth
- [ ] Tomcat



### Daily Log

#### 0420 (월)

- 기획서 분석
- 도메인 분석
- 개발환경 구축

#### 0421 (화)

- DB 설계
- CORS config 설정
- 프로젝트 기본 구조 작성 (Global Exception Handler 등)
- 클래스 구조에 대한 생각
- DAO, DTO 학습
- 생활코딩 MySQL 시청

#### 0422 (수)

- 전체 구조에 대한 생각
- DB 재설계
- DTO 사용 Wrapping
- 프로젝트 일지 작성 (이것)

#### 0423 (목)

- 



### 피드백

- 1주차




-----

## 고민사항

### DB 설계 진행사항

- 아이템 테이블은 하나로 하고, @Embedded를 이용하여 객체를 분야별로 나눈다. => DTO 설계로 변경
- 의문점1 : @Embedded 1:1 관계에서 중복되는 부분은 어떻게 처리??  => 하나 테이블로 통일 후 DTO 설계
- 일단하면서 수정해보자
- 의문점2 : delivery_type / badge 같이 DB에 배열로 저장할 수 없을까? 방식은?  => DTO로 한번더 Wrapping
- 생활코딩 DB 강의 들으며 리프레시
- 의문점3 : 카테고리 - 카드 구조에서 카드 전체 primary id로 접근하는 것과, 카테고리 id - 카드 카테고리 키로 접근하는 것중 뭐가 더 좋을까?
- 의문점4 : 데이터는 제공된 mockAPI에서 파싱해와야 하는 것 인가? 수동으로 가져와야 하는 것인가? => RestTemplate 으로 파싱해보자
