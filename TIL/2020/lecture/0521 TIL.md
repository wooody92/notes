## 오늘의 강의

### DB Index 복습

- 원본데이터가 아주 많고, 선택한 데이터(조건검색)의 결과가 아주 적을 때 인덱스를 만들면 좋다.
- 불필요한 인덱스는 만들지 않는 것이 좋다.
- Covering Index란?
- MySQL을 많이 사용하는 이유? OLTP이고 무료이기 때문, 간단한 쿼리에서는 가장 빠르다.
- Selectivity란? 전체 데이터에서 약 10% 일 경우에 인덱스를 사용한다. (남,녀와 같이 50% 경우 오히려 검색 시 느려진다.)
- 복합 인덱스 사용 시 주의 할 점? 생성 시 순서는 영향이 있다.
- 결론 : 검색 성능을 높이기 위해서 인덱스를 사용할 수 있으나, 아무렇게나 만든다고 향상되지는 않는다.

### Transaction

- 동시성 (Concurrency)
- **트랜잭션의 성질 (A.C.I.D)**
- CAP 이론
- DB는 Serialized 하기 위해 내부적으로 많은 동작이 발생한다.
- 너무 어렵다. 강의 다시보기.



#### 참고링크

- [https://lucas.codesquad.kr/course/masters-backend-java/RDBMS-%EC%9D%B5%ED%9E%88%EA%B8%B0/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98](
