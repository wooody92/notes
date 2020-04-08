### DB 생성 및 사용자 설정

- DB 생성

  ```mysql
  mysql> create database todo12;
  ```

- 사용자 생성

  ```mysql
  create user 'henry'@'%' identified by 'henry';
  Query OK, 1 row affected (0.00 sec)
  ```

- 생성한 DB에 사용자 권한 부여

  ```mysql
  grant all on todo12.* TO 'henry'@'%';
  Query OK, 1 row affected (0.00 sec)
  
  flush privileges;
  Query OK, 1 row affected (0.00 sec)
  ```

### EC2 mysql 원격 연결

- EC2 mysql 3306 포트 개방

- /etc/mysql/mysql.conf.d 경로 mysqld.cnf 주소 주석하여 포트 개방

  ```
  #bind-address = 127.0.0.1
  ```

- **위 방법은 인가되지 않은 사용자에게 모두 접근권한을 줄 수 있으므로 좋은 방법이 아니다.**

- mysql 재시작

  ```
  sudo service mysql restart
  ```

- 인텔리제이 application.properties 내용 추가

  ```
  # ec2 mySQL 연결
  spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
  
  # 접속 할 ip:port/database_name 
  spring.datasource.url=jdbc:mysql://54.180.75.159:3306/todo12
  
  # mysql name & password
  spring.datasource.username=henry
  spring.datasource.password=henry
  
  # 인텔리제이에 내장된 chema.sql을 사용
  spring.datasource.initialization-mode=embedded
  spring.datasource.data=classpath:schema.sql
  #spring.datasource.initialization-mode=always
  ```

  
