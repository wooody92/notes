## 오늘의 강의

### 야구 프로젝트

- Admin tool : 선수 데이터 입력, 통계보기 등
- OAuth를 별도의 라이브러리로 만들어 구현해보기 (다음 프로젝트를 위해서)
- DB : 선수정보, 게임정보 저장
- AWS 람다를 활용하면 서버없이 crontab 처럼 일정 주기로 업데이트 할 수 있다.
- EC2, RDS 1대 무료, 복제 불가, 오직 MySQL, 백업설정 불가 등 오직 기본 만 사용해야 무료
- 이번 배포는 임베디드 톰캣을 사용해서 로컬 jar 생성 후 s3 bucket의 파일 감지 후 서버에 배포

### VPC (Amazon Virtual Private Cloud)

- 기존에는 하나의 네트워크 망에 전체 사용자들이 사용했었다.
- 하나의 망을 사용하면 다른 사용자들의 서버 등을 전부 볼 수 있어서 보안상 사용자 전용 가상 네트워크로 변경했다.
- Global Service : Route53, CDN(Content Delivery Network), IAM
- Region service vs. AZ service
- VPC는 region 기반 서비스이다. VPC는 서브넷으로 나눌 수 있는데 서브넷은 AZ 기반 서비스이다.
- EC2는 AZ 기반 서비스이다. 즉, EC2는 VPC 서브넷과 연결된다.

### VPC 생성

- 서브넷 a,b,c는 사용자마다 다르게 보인다. (서브넷 a에 사용자가 몰리는 것을 방지, a,b,c는 물리적인 region을 의미한다.)
- CIDR 블록 : 10.0.0.0/16 -> 사용가능 아이피 갯수 : 2^16 - 5(브로드 캐스트 및 AWS에서 사용하는 아이피)
- 10.1.1.0/24 -> 256, 2^8 가변 비트, 가변비트는 0으로 표기해야 한다.
- VPC 피어링 : 두 VPC 연결 할 때
- S3는 별도의 네트워크 망에 존재한다.
- VPC Service Endpoint : S3와 같이 외부 망을 내부 망으로 변경 할 수 있다.
- VPC 생성 후 할일 : 인터넷 게이트웨이 생성 및 VPC에 연결 -> 폐쇄망이기 때문에 인터넷에 연결해야 사용자가 접속 가능하기 때문이다.
- 서브넷은 VPC CIDR의 부분집합 이어야 한다. 즉, 포함관계이다.
- 서브넷마다 고유한 NACL을 가진다. 시큐리티 그룹에 도달하기 전에 처리.
- 라우팅 테이블 : VPC에 생성한 서브넷 중 어느곳으로 연결할 지 결정한다.
- Route Table : Local로 사용하는 아이피는 보통 지정되어있다. (10.x.x.x) 그렇지 않으면 외부에서 사용하는 IP와 충돌 시 로컬로 타고 들어가기 때문이다.

#### 참고링크

- [https://lucas.codesquad.kr/course/masters-backend-java/AWS-Basic/VPC-%EC%8B%A4%EC%8A%B5](https://lucas.codesquad.kr/course/masters-backend-java/AWS-Basic/VPC-실습)
- https://www.44bits.io/ko/post/understanding_aws_vpc
