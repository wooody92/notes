## 오늘의 강의

### 서버관리

- 여유가 있다면 서버는 NGinx tomcat 1대, DB Server 1대 나눠서 관리한다.

- DB가 랜섬웨어에 공격받으면 서비스 끝장난다. 방지책으로 백업 데이터를 만든다.

- 백업 데이터는 주기적으로 백업하여 다른 서버에 보관한다.

- 서버(= 리소스, 돈)가 많으면 백업 주기를 줄일 수 있고, 리스크를 낮출 수 있다.

- DB 분리는 필수다.

- 서버가 여러개라면?

  DB(master, first) - Web Server(NGinX, Spring) - DB replica(복제, 이중화, slave, secondary)

  DB(master, first) - Web Server(NGinX) - DB replica(복제, 이중화, slave, secondary) - Web Server(Spring)

### 배포

- RDS 사용 시 복제옵션 없이 제일 작은거 한대 사용해야 과금없다.

- linux cmd : tmux (가상 스크린)

- war Build 할때 embedded tomcat 빼고 빌드해야 가볍다.

- main에서 override 안해도 extend 만 해도 정상동작하긴 한다.

- 아래는 build는 default가 jar이지만 war로 id 설정 변경하면 동일하다.

  ```
  ./gradlew bootWar = ./gradlew build
  ```

- EC2가 이상할 땐 톰캣로그 등 AWS에서 제공하는 로그를 확인한다.

- 자동화 배포를 위한 shell script 작성

- 톰캣설치는 wget 설치link 으로 다운받고 tar 명령어로 압축풀기

- 톰캣 종료 ./shutdown.sh

- 빌드해서 생긴 .war 파일을 톰캣 root 폴더로 이동

- Git clone - tomcat 중지 - build 후 war 파일 tomcat 디렉토리로 이동 - 톰캣 실행

- git rev-parse HEAD와 git rev-parse origin/HEAD 비교하여 업데이트 커밋이 있는지 비교할 수 있다.

  ```
  if [[ $a -eq $b ]]; then
  ```

- 위 방법을 사용하여 불필요한 빌드를 줄일 수 있다.

- Crontab 사용하여 시간단위로 sh 파일 자동 실행 할 수 있다.

- 적당한 시간을 정하여 실행한다. 

- 리다이렉트 시켜줘야 한다.

  ```
  date >> /home/ubuntu/date.log
  ```

  ```
  */5 * * * * /home/ubuntu/build.sh >> build.log 2>&1
  ```

- 2>&1 에러 메세지 로그기록
