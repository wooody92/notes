## AWS EC2

### EC2 연결하기

1. EC2 인스턴스를 생성한다. 스프링 부트를 사용하려면 사용자 지정 TCP 8080 포트를 열어주어야 한다.

   <img width="970" alt="스크린샷 2020-03-29 오후 5 24 09" src="https://user-images.githubusercontent.com/58318041/77844466-1fe6fa00-71e2-11ea-87d2-c25108652eb4.png">

2. SSH로 접속하기 위해 인스턴스 생성시 저장한 인스턴스 키를 적당한 디렉토리로 이동한다.

3. 해당 인스턴스 키를 보호하기 위해 읽기전용으로 수정한다.

   ```
   chmod 400 henry-keypair.pem
   ```

4. 인스턴스 키가 포함된 디렉토리에서 해당 인스턴스를 ssh를 이용하여 접속한다.

   ```
   ssh -i "henry-keypair.pem" ubuntu@ip(할당받은)
   ```

   <img width="943" alt="스크린샷 2020-03-29 오후 5 00 05" src="https://user-images.githubusercontent.com/58318041/77844391-6daf3280-71e1-11ea-8ea0-2cc089901771.png">

5. 인스턴스 우분투 접속 완료
<img width="653" alt="스크린샷 2020-03-29 오후 5 49 46" src="https://user-images.githubusercontent.com/58318041/77844961-d26c8c00-71e5-11ea-8bae-66fc508e9cdc.png">

------

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

4. 프로젝트 디렉토리로 이동 후 빌드 후 런

   ```
   ./gradlew build
   ./gradlew bootRun
   ```

5. 정상 빌드

   <img width="653" alt="스크린샷 2020-03-29 오후 5 17 43" src="https://user-images.githubusercontent.com/58318041/77844428-abac5680-71e1-11ea-873b-5a17fc30a02e.png">

6. 정상 접속 확인

   <img width="726" alt="스크린샷 2020-03-29 오후 5 22 56" src="https://user-images.githubusercontent.com/58318041/77844445-f4640f80-71e1-11ea-8222-325b1c9ca57a.png">

#### 참고 링크

- https://opentutorials.org/course/2717/11280
- 호눅스의 유튜브 비밀링크
