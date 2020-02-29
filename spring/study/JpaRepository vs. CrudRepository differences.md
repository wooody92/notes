### paRepository 와 CrudRepository 의 차이점

1. CrudRepository <- PagingAndSortingRepository <- JpaRepository 인터페이스 상속

<img width="710" alt="스크린샷 2020-02-29 오후 7 24 13" src="https://user-images.githubusercontent.com/58318041/75605786-3dfd0400-5b29-11ea-9a07-88359c10e5f8.png">

2. 기능

   - CrudRepository : CRUD 관련 기능들을 제공

   - PagingAndSortingRepository : paging 및 sorting 관련 기능들 제공

   - JpaRepository : JPA 관련 특화 기능들 (flushing, 배치성 작업 등) + (CrudRepository와 PagingAndSortingRepository의 기능들) 제공

3. 출처

   ```
   https://blog.naver.com/writer0713/221587319282
   ```
