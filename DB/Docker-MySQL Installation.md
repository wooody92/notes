## Docker MySQL Installation

### Docker 설치

- Docker 홈페이지 다운로드 후 설치한다. docker 버전으로 정상 설치 확인한다.

  ```
  docker --version
  ```

### MySQL 다운로드 및 컨테이너 생성

- MySQL 이미지 다운로드 및 컨테이너를 생성한다.

  ```
  docker run --name <container-name> -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<mysql-password> -d mysql:5.7.29 --character-set-server=utf8mb4 --collation-server=utf8mb4_unlsicode_ci
  ```

- Docker 컨테이너 목록을 확인한다.

  ```
  docker ps -a
  ```

- 생성된 특정 컨테이너 실행하기

  ```
  docker start <container-name>
  ```

### Docker 컨테이너 실행하기

- 실행 중인 컨테이너 접속하기

  ```
  docker exec -it <container-name> env TERM=xterm-256color script -q -c "/bin/bash" /dev/null
  ```

### MySQL 기본 설정

- 한글 설정 : UTF8 설정
- DB 생성하기
- User 생성 후 권한부여



#### 참고링크

- https://gist.github.com/ksundong/7f695db1486d1ab28f854d3f0d1dcf66
- http://jmlim.github.io/docker/2019/07/30/docker-mysql-setup/
- [https://velog.io/@swhybein/Docker-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0](https://velog.io/@swhybein/Docker-설치하기)

