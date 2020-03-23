### 오늘의 강의

### MySQL Database

- 요구사항 분석 -> ER diagram 작성 -> 코드작성

- ssh (port 20), mysql (port 3306)

- mysql은 기본적으로 외부 접속 막혀있다.

- sudo vi /etc/mysql/my.cnf 파일에 bind-address = 0.0.0.0 추가

  https://medium.com/code-kings/mysql-how-to-connect-to-your-ubuntu-vm-remotely-using-mysql-workbench-from-oracle-e280602d7ff9

- Mysql 사용자 생성 -> 데이터베이스 생성 -> 권한부여 

- 워크벤치를 우분투 mysql 접속해 사용한다면 로컬ip가 아니라 우분투 ip를 가져와야함

- DB에서 NULL은 비어있다가 아닌 정해지지 않음을 뜻한다.

- forein key와 primary key를 통해 join 할 수 있다.

- 외래키 제약조건 - NULL을 넣을 수 있다. primary key에 없는 것은 참조할 수 없다.

- 참조 무결성 제약조건

- 조인 조건 : ON, 필터조건 : WHERE

- 데이터 모델링? 필요한 데이터만 뽑아내는 작업, 적으면 적을수록 좋다.

- ERD 모델링 실습
