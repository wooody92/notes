# ISSUE TRACKER

- https://github.com/codesquad-member-2020/issue-tracker-12



## Study Keyword

- [x] `JPQL`
- [x] `fetch join`
- [x] `Lazy Loading`과 `proxy 객체`
- [x] `Entity Manager`
- [x] `Enum`
- [x] `@Enumerated(EnumType.STRING)`
- [x] `Static Factory Method`
- [x] `Patch vs Put`
- [x] `Entity vs. Value Object`
- [x] `Lazy Loading`과 `proxy 객체`
- [x] `Query DSL` 동적쿼리 처리
- [x] `Collection Query` 최적화
- [x] `Unit test`



## ERD

<img width="979" alt="스크린샷 2020-06-24 오후 3 30 24" src="https://user-images.githubusercontent.com/58318041/85940404-18f19400-b957-11ea-8c97-db2f1fa9c450.png">



## Goal

- Unit Test
- JPA
- DDD
- 쿼리 최적화



## Daily Log

#### 0608 (월)

- 호눅스 강의
- 개발환경 설정
- 팀원 단합회식

#### 0609 (화)

- 기획서 분석
- OAuth 구현
- JPA 성능 최적화 학습

#### 0610 (수)

- 기획서 분석
- 도메인 모델링
- ERD 작성
- Graph QL 학습
- 도메인 엔티티 개발
- Mock data 입력

#### 0611 (목)

- 이슈 목록 화면 API 구현
- 이슈, 사용자, 라벨, 마일스톤 DTO 생성

#### 0612 (금)

- 데모
- 이슈 OPEN/CLOSE 필터 추가
- 이슈 리스트 페이징 처리

#### 0615(월)

- 레이블 테이블 변경 (컬럼 추가)
- 레이블 조회, 생성, 삭제, 수정 API 구현
- API 기능서 작성

#### 0616(화)

- 이슈 생성 API 구현
- 유저 목록 API 구현
- 마일스톤 목록 API 구현
- 이슈 상세 조회 API 구현
- 이슈 제목 수정 API 구현
- 이슈 내용 수정 API 구현
- 이슈 OPEN/CLOSE API 구현

#### 0617(수)

- 현재 이슈에 Labels 변경 API
- 현재 이슈에 Assignees 변경 API
- 호눅스 알고리즘 강의
- 백엔드 회식

#### 0618(목)

- 현재 이슈에 Milestone 변경 API
- 코멘트 추가 API
- 코멘트 제거 API
- 코멘트 변경 API

#### 0619(금)

- JPA 강의 - 컬렉션 조회 쿼리 최적화
- 데모 

#### 0621(일)

- 2주차 리뷰요청
- JPA 강의

#### 0622(월)

- 호눅스 강의 - DevOps
- Query DSL 학습
- Query DSL 개발환경 설정

#### 0623(화)

- Query DSL 학습
- 이슈 필터링 API
- 이슈 조회 쿼리 최적화 진행
- 마일스톤 API

#### 0624(수)

- 단위 테스트 작성

#### 0625(목)

- Github Action 배포 자동화
- 데모

## Issues

1. `Child Entity: label`에서 `Parent Entity: issue`와 연관관계 테이블로 `issue`가 갖고있는 `label's f.k`를 제거 할 수 없는 문제

   - `label Entity`에서 `issue`에 접근하여 해당 `label`목록 삭제하여 진행

   - [참고 링크](https://www.it-swarm.dev/ko/java/jpa-및-해당-조인-테이블-행에서-manytomany-관계가있는-엔티티를-제거하는-방법은-무엇입니까/967305855/)

    



## API 명세
- https://github.com/codesquad-member-2020/issue-tracker-12/issues/46

| URL                               | Method | Description                      | Response Code |
| --------------------------------- | ------ | -------------------------------- | ------------- |
| /issues                           | GET    | 이슈 목록                        | 200           |
| /issues                           | POST   | 이슈 생성                        | 200           |
| /issues/{issue_id}                | GET    | 이슈 상세 조회                   | 200           |
| /issues/{issue_id}/title          | PUT    | 이슈 제목 변경                   | 200           |
| /issues/{issue_id}/content        | PUT    | 이슈 내용 변경                   | 200           |
| /issues/{issue_id}/status         | PUT    | 이슈 상태 변경 (OPEN/CLOSE)      | 200           |
| /issues/{issue_id}/labels         | PUT    | 이슈 레이블 변경                 | 200           |
| /issues/{issue_id}/assignees      | PUT    | 이슈 담당자 변경                 | 200           |
| /issues/{issue_id}/milestone      | PUT    | 이슈 마일스톤 변경               | 200           |
| /issues/{issue_id}/comment        | POST   | 이슈 코멘트 생성                 | 200           |
| /issues/{issue_id}/comment        | PUT    | 이슈 코멘트 변경                 | 200           |
| /issues/{issue_id}/comment        | DELETE | 이슈 코멘트 삭제                 | 200           |
| /issues/status                    | PUT    | 여러 이슈 상태 변경 (OPEN/CLOSE) | 200           |
| /issues/search                    | GET    | 이슈 필터링 조회                 | 200           |
| /labels                           | GET    | 레이블 목록                      | 200           |
| /labels                           | POST   | 레이블 생성                      | 200           |
| /labels/{label_id}                | PUT    | 레이블 수정                      | 200           |
| /labels/{label_id}                | DELETE | 레이블 삭제                      | 200           |
| /milestones                       | GET    | 마일스톤 목록                    | 200           |
| /milestones                       | POST   | 마일스톤 생성                    | 200           |
| /milestones/{milestone_id}        | PUT    | 마일스톤 수정                    | 200           |
| /milestones/{milestone_id}        | DELETE | 마일스톤 삭제                    | 200           |
| /milestones/{milestone_id}/status | PUT    | 마일스톤 상태 변경 (OPEN/CLOSE)  | 200           |
| /users                            | GET    | 유저 목록                        | 200           |

