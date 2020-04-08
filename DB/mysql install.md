### MySQL 설치

- version 확인

  ```
  sudo apt-cache search mysql-server
  ```

- 설치 ( -5.7 생략 가능 )

  ```
  sudo apt-get install mysql-server-5.7
  ```

- 접속하기

  ```
  sudo mysql
  ```

- 비밀 번호 설정

  소켓 플러그인 방식 -> 패스워드 방식으로 변경

  ```mysql
  mysql> update mysql.user set plugin='mysql_native_password' where user='root';
  Query OK, 1 row affected (0.01 sec)
  Rows matched: 1  Changed: 1  Warnings: 0
  
  mysql> update mysql.user set authentication_string=PASSWORD('root') where user='root';
  Query OK, 1 row affected, 1 warning (0.01 sec)
  Rows matched: 1  Changed: 1  Warnings: 1
  
  mysql> flush privileges;
  Query OK, 0 rows affected (0.00 sec)
  ```

- 비밀번호로 접속하기

  ```mysql
  mysql -u root -p
  ```

### MySQL 한글 설정

- 현재 status 확인

  ```mysql
  mysql> status
  --------------
  mysql  Ver 14.14 Distrib 5.7.29, for Linux (x86_64) using  
  Connection:		Localhost via UNIX socket
  Server characterset:	latin1
  Db     characterset:	latin1
  Client characterset:	utf8
  Conn.  characterset:	utf8
  --------------
  ```

- /etc/mysql/ 경로의 my.cnf 내용 추가

  Sudo 명령어로 열어야 저장 가능하다.

  ```
  sudo vi my.cnf
  
  [client]
  default-character-set = utf8
  
  [mysqld]
  init_connect = SET collation_connection = utf8_general_ci
  init_connect = SET NAMES utf8
  character-set-server = utf8
  collation-server = utf8_general_ci
  
  [mysqldump]
  default-character-set = utf8
  
  [mysql]
  default-character-set = utf8
  ```

- mysql 재시작

  ```
  sudo mysql restart
  ```

- mysql 접속 후 변경값 확인

  ```mysql
  mysql> status
  --------------
  mysql  Ver 14.14 Distrib 5.7.29, for Linux (x86_64) using  EditLine wrapper
  
  Protocol version:	10
  Connection:		Localhost via UNIX socket
  Server characterset:	utf8
  Db     characterset:	utf8
  Client characterset:	utf8
  Conn.  characterset:	utf8
  --------------
  ```

#### 참고링크
- https://github.com/Hyune-c/TIL/blob/master/BackEnd/Setup/Mysql.md
