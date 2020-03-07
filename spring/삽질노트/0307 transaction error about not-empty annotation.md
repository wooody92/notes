### 오늘의 삽질

1. 이슈

   - Question Entity에 deleted 데이터 추가 후 .save 시 아래 transaction 에러 발생

   ```java
   @NotEmpty
   private boolean deleted;
   ```

   ```html
   Could not commit JPA transaction; nested exception is javax.persistence.RollbackException: Error while committing the transaction
   ```

2. 솔루션

   - NotEmpty Annotation 제거 후 정상동작

   ```java
   private boolean deleted;
   ```

