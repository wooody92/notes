### 오늘의 강의

### 배경지식

1. Elasticsearch
2. Spring Data Project 란?
3. Spring의 3대 요소: IoC, AOP, PSA
4. JPA
5. JpaRepository 지원
6. PagingAndSortingRepository 지원
   1. 페이지를 만들기 위한 쿼리 등 기능들이 구현되어 있다. 
   2. Page Query 어떻게 구현할 수 있을까?
   3. 댓글의 댓글은 어떻게 구현할 수 있을까?

### Spring Data JDBC

1. JDBC 기반 repository를 쉽게 구현할 수 있게 도와주는 툴
2. CrudRepository, @Query, MyBatis 등 지원
3. ORM을 지원해주는 -> MyBatis vs. Hibernate (JPA의 구현체)
4. 한국에서는 Mybatis 많이 쓰는데, 글로벌에서는 Hibernate 더 많이 쓴다.
5. **Transaction의 4가지 성질**
6. Eventual Consistency -> Consistency를 언젠지는 모르지만 보장해 준다.
7. qna 프로젝트에서 대상 비교할 때(.equals) id를 비교 안하는 이유?
   1. 자동 생성으로 DB 생성 전에 비교한다면, null 값 받을 수 있음
   2. 유니크한 값 (객체가 가지는)으로 비교하는 것이 컨벤션 


#### 참고 블로그

https://lucas.codesquad.kr/course/masters-backend-java/Spring-학습/Spring-Data-JDBC-시작하기
