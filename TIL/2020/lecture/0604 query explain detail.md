# 오늘의 강의

## EXPLAIN

- `explain` `inner join` 하면 논리적으로 순서가 상관없기 때문에 효율적인(데이터가 많은)것 부터 순서가 정해진다.
- `explain` `left outer join` 하면 순서가 강제로 정해지기 때문에 성능이 나빠질 수 있다.

### SLECT_TYPE

- `DERIVED` `From`의 서브 쿼리
- `DEPENDANT SUBQUERY` 제곱형태로 조회를 해서 성능이 엄청 느리다. `Join`으로 풀어낼 수 있으면 풀어내자.

### TYPE

- 실제 데이터를 읽는 방법
- `SYSTEM`, `CONST`, `REF`, `RANGE`, `INDEX`, `ALL` 등이 있다. (좌측붜 빠른 순서)
- `INDEX`는 `INDEX FULL SCAN` 빠르지 않다.
- `Selectivity` 등 `MySQL`이 효율적으로  `index`를 사용할지 말지 결정해서 처리한다.

### KEY_LENGTH

- 복합 인덱스 두번째 필드 단독으로 사용할  수 없다.

### ROW

- 대략적인 통계정보가 출력된다.

### 결론

- `EXPALIN`을 통해 쿼리 최적화 성능 개선을 위해 원인을 분석 할 수 있다.

#### 참고 링크

- [https://lucas.codesquad.kr/course/masters-backend-java/RDBMS-%EC%9D%B5%ED%9E%88%EA%B8%B0/%EC%BF%BC%EB%A6%AC-%ED%8A%9C%EB%8B%9D-%EA%B8%B0%EC%B4%88](https://lucas.codesquad.kr/course/masters-backend-java/RDBMS-익히기/쿼리-튜닝-기초)

