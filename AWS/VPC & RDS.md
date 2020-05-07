## AWS 인프라 구축

### VPC 생성

- 아래 링크에서 8번 단계까지 진행한다.

- [https://lucas.codesquad.kr/course/masters-backend-java/AWS-Basic/VPC-%EC%8B%A4%EC%8A%B5](https://lucas.codesquad.kr/course/masters-backend-java/AWS-Basic/VPC-실습)

- 단, 8번 단계에서 Subnets -> my-private-subnet -> Route Table -> Target에 미리 생성하여 서브넷과 연결 할 EC2 추가한다. (Destination : 0.0.0.0/0)

  <img width="776" alt="스크린샷 2020-05-07 오후 6 19 34" src="https://user-images.githubusercontent.com/58318041/81277426-5ccec800-908f-11ea-9a46-c37338ed7b6d.png">

### EC2 생성

- 기존의 방식대로 생성한다.
- Network : 위에서 생성한 VPC 선택
- Subnet : VPC의 public subnet
- Auto-assign public IP : Enable

### RDS 생성

- Standard Create -> MySQL -> Free tier 선택한다.

  <img width="761" alt="스크린샷 2020-05-07 오후 6 22 19" src="https://user-images.githubusercontent.com/58318041/81277676-b46d3380-908f-11ea-8f36-2fde7717f171.png">

- DB Identifier : RDS 구분 할 이름을 입력한다.

- Credentails Setting : DB에 연결 할 유저 아이디와 패스워드를 입력한다.

- DB instance size : Free Tier이기 때문에 t2.micro 선택한다.

- Storage : 기본 default 값 설정후, 추가기능은 모드 Uncheck 한다.

- Connectivity : 위에서 생성한 VPC 클릭한다.

- Additional connectivity configuration :

  - subnet group : 좌측 상단 subnet groups에서 서브넷 그룹을 생성 할 수있다. 최소 2개의 서브넷이 있어야 생성 할 수 있다. 해보지는 않았지만, 필수 선택사항은 아닌듯 하다.
  - Publicly accessible : 별다른 이유가 없다면, 기본 설정값인 No 선택한다.
  - VPC security groups : 
  - Availablity Zone : 생성한 private 서브넷 존 할당한다.
  - Database port : MySQL 이므로 3306 포트 할당한다.

- Database authentication : Password authentication 선택한다.

- Additional configuration : 추가적으로 필요한 기능을 선택할 수 있다.

  - DB parameter group : UTF8 설정을 위해, character-set 선택한다.
  - Parameter groups에서 character-set 관련 항목의 values : utf8 설정한다.

- RDS 생성완료! EC2 내에서 명령어에 endpoint를 이용하여 접속 할 수 있다.

  ```
  sudo mysql -u admin -p --host "endpoint url"
  ```

#### 참고링크
- https://www.44bits.io/ko/post/understanding_aws_vpc
