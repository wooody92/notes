### EC2 - RDS CSV Insert

```
mysql -u <RDS-userId> -p -h <RDS-Endpoint> --local-infile <DB-name> -e "LOAD DATA LOCAL INFILE '<file.csv>' INTO TABLE <table-name> FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'"
```

- 예시

```
mysql -u admin -p -h baseball08.ckp6apk75dyc.ap-northeast-2.rds.amazonaws.com --local-infile airbnb02 -e "LOAD DATA LOCAL INFILE '~/github/airbnb-02/BE/csv/mock_host.csv' INTO TABLE host FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n'"
```

- MySQL-CSV 입력

```
LOAD DATA LOCAL INFILE '/mock_host.csv' INTO TABLE host FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
```
