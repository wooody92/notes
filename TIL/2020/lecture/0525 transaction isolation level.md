## 오늘의 강의

### @Transcation

- Transaction은 Serialized하다.
- P1 (Dirty Read Problem) : DB 변경된 값을 읽은 문제
- P2 (Non-repeatable Read Problem) : 커밋 한 값을 읽었을 때 값이 바뀌는 문제
  - Transaction의 성질인 Isolation에 위배된다.
  - 해결책은? 읽었을 때 다르면 롤백해버린다.
- P3 (Phantom Read Problem) : 통계나 분석 등 수행하는 쿼리에서 잘못된 값이 들어오는 경우
  - 데이터는 변하지 않는데 통계값만 바뀌는 경우

### Transaction Mode (Isolation Level)

- Transactional Level은 스프링이 아닌 DB의 설정이다. `@Transactional`을 사용하면 DB의 설정된 Default 값을(MySQL default: Repeatable Read) 사용한다.
- READ-UNCOMMITTED
  - 커밋되지 않은 데이터도 읽을 수 있다. 성능이 매우 좋다.
  - 전혀 isolation 하지 않아 transaction에 위배된다.

- READ-COMMITTED
  - 커밋 된 데이터만 읽을 수 있다.
- REPEATABLE-READ
  - 다른쪽에서 커밋 된 데이터도, 내 Transaction 내에서는 변경사항이 반영되지 않는다.
  - 한번 시작 된 Transaction 중간에는 외부에서 데이터가 바뀌어도 방해받지 않는다.
- SERIALIZABLE
  - 쓰기와 읽기를 동시에 사용 할 수 없다. (순서에 상관없이 동시에 사용 할 수 없다.)
  - 여러명이서 동시에 읽기는 가능하다.
  - 한 쪽에서 데이터를 변경하면, 변경이 끝날 때 까지 읽을 수 없다. Lock이 걸린다. 계속 두면 Deadlock 걸린다.
  - 엄청 느리다. 동시성 (Concurrency) 레벨

