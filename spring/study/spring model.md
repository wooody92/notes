## Spring Model

- Spring Framework의 MVC에서 Model은 Service, DAO, DTO로 나눌 수 있다.

-----

### DAO (Data Access Object)

- Repository
- JdbcTemplate
- DB를 사용해 데이터를 조작하거나 조회하는 기능을 (CRUD) 담당
- DAO를 통해 DB에 접근한다.

### DTO (Data Transfer Object)

- Entity
- VO (Value Object)
- DB의 데이터를 매핑하기 위한 데이터 객체
- DB에서 데이터를 얻어 컨트롤러나 서비스에서 사용되는 객체이다.

### Service

- Service
- 비즈니스 로직을 처리하는 부분
- 컨트롤러가 리퀘스트를 받으면 작성된 적절한 서비스에 전달하여 로직을 처리한다.

#### 참고 링크

- https://lazymankook.tistory.com/30
