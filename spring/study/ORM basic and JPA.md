### 쿼리 또는 SQL

- CRUD(create, read or retrieve, update, delete)
- create - insert query
- read - select query
- update - update query
- delete - delete query

### ORM (Object Relational Mapping)

- 자바 객체와 테이블 맵핑을 통해 DB 쿼리를 손쉽게 도와주는 프레임워크
- 객체가 테이블이 되도록 맵핑시켜주는 것

### JDBC (Java Database Connectivity)

- DB에 접근할 수 있도록 Java에서 제공하는 API

### JPA (Java Persistance API)

- ORM을 사용하기위한 인터페이스를 모아놓은 것
- Hibernate, OpenJPA 등의 구현체가 있음 (ORM Framework라고도 부름)
- @Entity, @Id, @Column 등..

**Hibernate가 지원하는 메서드 내부에서는 JDBC API가 동작하고 있으며, 단지 개발자가 직접 SQL을 직접 작성하지 않을 뿐이다.**

-----

참고 블로그

```
https://victorydntmd.tistory.com/195
```

