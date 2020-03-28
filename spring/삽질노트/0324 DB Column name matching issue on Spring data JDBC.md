### 오늘의 삽질

1. 이슈

   - Spring Data JDBC에서 DB 컬럼명 생성시 소문자 중간에 대문자가 들어가면 자동으로 _를 추가하여 생성하는 듯 하다.
   - DB에서 대소문자 구분을 _이용하여 사용하는 듯?

   ```java
   public class User {
       @Id
       Long id;
       String userId;
       String password;
       String name;
       LocalDate createdDate;
   
       public String getUserId() {
           return userId;
       }
     
       public void setUserId(String userId) {
           this.userId = userId;
       }
     ....
   }
   ```

   ```java
   CREATE TABLE user (
     id bigint NOT NULL AUTO_INCREMENT,
     userId varchar(64),
     password varchar(64),
     name varchar(64),
     PRIMARY KEY (id)
   );
   ```

   ```java
   <Error Message>
     Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'h2Console' defined in class path resource [org/springframework/boot/autoconfigure/h2/H2ConsoleAutoConfiguration.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [org.springframework.boot.web.servlet.ServletRegistrationBean]: Factory method 'h2Console' threw exception; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'dataSource' defined in class path resource [org/springframework/boot/autoconfigure/jdbc/DataSourceConfiguration$Hikari.class]: Initialization of bean failed; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.boot.autoconfigure.jdbc.DataSourceInitializerInvoker': Invocation of init method failed; nested exception is org.springframework.jdbc.datasource.init.ScriptStatementFailedException: Failed to execute SQL script statement #2 of URL [file:/Users/henry_yoon/Documents/signup-12/BE/signup12/out/production/resources/schema.sql]: CREATE TABLE interest ( id bigint NOT NULL AUTO_INCREMENT, userId bigint NOT NULL, interest varchar(25), PRIMARY KEY (id), CONSTRAINT fk_interest_to_user FOREIGN KEY (user_id) REFERENCES user (id) ON DELETE RESTRICT ON UPDATE RESTRICT ); nested exception is org.h2.jdbc.JdbcSQLException: Column "USER_ID" not found; SQL statement:
   ```

2. 솔루션

   - DB 테이블 생성시  user_id로 _ 추가하여 생성하여 매칭에러 해결했다.

   ```java
   CREATE TABLE user (
     id bigint NOT NULL AUTO_INCREMENT,
     user_id varchar(64),
     password varchar(64),
     name varchar(64),
     PRIMARY KEY (id)
   );
   ```

#### 참고링크

```
Jpa에서 자동으로 만들어주는 테이블의 경우 createDate 란 이름의 칼럼은 createdDate라는 이름 그대로 칼럼을 만들어준다.
참조 타입의 칼럼명에 _ 를 쓰려면 @Column을 사용해서 이름을 지정한다.
Data Jdbc에선 name 중간에 대문자가 있으면 _소문자로 기본 변환한다. (칼럼명 생성 규칙이 반대로 되어 있는 것 같은?)
createdDate는 created_date로 쿼리를 만든다. @Column("createdDate")과 같이 재지정해야 해결된다.
```

- 출처 : https://luvstudy.tistory.com/82
