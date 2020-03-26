### SQL 기본 문법

- SELECT * FROM table1

  Table1 전체 정보를 가져온다.

- SELECT * FROM table1 LEFT JOIN table2 ON table1.table2_id = table2.tid

  가져온 table1의 정보에 table2를 연결하는데, ON 뒤에 조건에 맞는 데이터를 기준으로 가져온다.

  매칭되는 행이 없는 경우 NULL을 가져온다.

- SELECT * FROM TABLE LEFT JOIN table2 ON table1.table2_id = table2.tid WHERE table1.table2_id =1

  가져온 데이터중 WHERE 뒤 조건인 정보만 불러온다.

- Schema.sql 에서 interest 용 table 하나 더 생성 후 관계로 연결 (Join) ?
  - primary key => User
  - foreign key => Interest
