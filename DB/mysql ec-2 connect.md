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

- **위 방법은 인가되지 않은 사용자에게 모두 접근권한을 줄 수 있으므로 좋은 방법이 아니다.**

- ssh 터널링 혹은 ec2 보안그룹에서 3306포트 내 ip만 허용으로 변경하여 보호할 수 있다. 

- /etc/mysql/mysql.conf.d 경로 mysqld.cnf 주소 주석하여 포트 개방

  ```
  #bind-address = 127.0.0.1
  ```

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
  spring.datasource.initialization-mode=always
  spring.datasource.data=classpath:schema.sql
  #spring.datasource.initialization-mode=embedded
  ```

- spring.datasource.initialization-mode=always의 경우 아래와 같이 schema.sql에서 초기화 시켜주지않고 테이블을 생성하면 충돌 에러가 발생한다.

  ```sql
  DROP TABLE IF EXISTS category;
  DROP TABLE IF EXISTS card;
  DROP TABLE IF EXISTS history;
  DROP TABLE IF EXISTS user;
  
  CREATE TABLE category  (
    id int primary key auto_increment,
    name varchar(32) not null,
    cards_count int,
    valid boolean
  );
  
  CREATE TABLE card  (
    id int primary key auto_increment,
    title varchar (32),
    content varchar (32),
    author varchar (32),
    create_time datetime,
    modified_time datetime,
    category int references category(id),
    category_key int
  );
  
  --on delete cascade on update cascade
  
  CREATE TABLE history  (
    id int primary key auto_increment,
    user_id varchar (32),
    action varchar (32) not null,
    title varchar (32),
    from_category varchar (32),
    to_category varchar (32)
  );
  
  CREATE TABLE user  (
    id int primary key auto_increment,
    user_id varchar (32) not null,
    password varchar (32) not null
  );
  ```

- 실 배포 서버에서 서버를 재시작 할때마다 DB를 초기화하는 것은 굉장히 위험한 짓이다. 서버 재시작마다 DB 초기화는 테스트 개발에서만 사용하도록 하자. 
