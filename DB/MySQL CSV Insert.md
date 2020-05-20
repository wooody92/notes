### Docker MySQL csv 파일 입력하기

- 로컬의 csv 파일을 docker로 복사한다.

  ```
  docker cp ~/<csv-file-name>.csv <container-id>:/
  ```

- Docker - MySQL 접속 후 사용 할 DB 선택한다.

- csv 사용 될 Table 생성한다. 단, 컬럼 순서는 일치해야 한다.

- 해당 테이블에 csv 파일 입력한다.

  ```
  LOAD DATA LOCAL INFILE '/airbnb-host.csv' INTO TABLE host FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
  ```

  
