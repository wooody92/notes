## AWS EC2

### EC2 Spring Boot Build

1. EC2 서버에 JDK를 받기 위해 아래 명령어를 통해 업데이트 및 다운받는다.

   ```
   sudo apt-get update
   sudo apt-get install openjdk-8-jdk -y
   ```

2. github repository를 clone 해 오기위한 적당한 위치에 디렉토리를 생성 후 이동한다.

   ```
   mkdir doc
   cd doc
   ```

3. 생성한 디렉토리로 이동하여 repository clone 한다.

   ```
   git clone https://github.com/codesquad-member-2020/signup-12.git
   ```

4. 프로젝트 디렉토리로 이동 후 테스트 없이 빌드 후 런

   ```
   ./gradlew build -x test
   ./gradlew bootRun
   ```

5. 정상 빌드

   <img width="653" alt="스크린샷 2020-03-29 오후 5 17 43" src="https://user-images.githubusercontent.com/58318041/77844428-abac5680-71e1-11ea-873b-5a17fc30a02e.png">

6. 정상 접속 확인

   <img width="726" alt="스크린샷 2020-03-29 오후 5 22 56" src="https://user-images.githubusercontent.com/58318041/77844445-f4640f80-71e1-11ea-8222-325b1c9ca57a.png">

### Background 배포

- ```
  ./gradlew build -x test
  ```

- 빌드가 되고 나면 `{프로젝트}/build/libs` 안에 `.jar` 파일이 생기게 된다.

- nohup 명령어는 터미널이 꺼지더라도 백그라운드로 톰캣이 실행될 수 있도록 해주는 명령어다.

- ```
  nohup java -jar dust12-0.0.1-SNAPSHOT.jar &
  ```

- 마지막에 & 꼭 붙이기

### 백그라운드 nohup 종료

- 쉘 스크림트 파일명으로 PID 번호 확인 (java -jar)

  ```
  ps -ef | grep todo-12-0.0.1-SNAPSHOT.jar
  ```

-  해당 포트 종료

  ```
  Kill -9 PID번호
  ```

  

#### 참고 링크

- https://opentutorials.org/course/2717/11280
- 호눅스의 유튜브 비밀링크
- https://gist.github.com/jypthemiracle/249ca7052659502868faab0dab1819d8
