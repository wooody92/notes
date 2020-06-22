# 오늘의 수업

## DevOps



### 개요

- 개발 운영
- 어플리케이션과 서비스를 빠른 속도로 제공하는 것이 목표

### DevOps의 적용

- 개발팀 + 운영팀 단일화
- 개발 - 테스트 - 배포 - 운영 전체를 팀에서 책임진다.
- 프로세스 자동화

### 애자일 개발 : Scrum

- 스프린트 : 짧은 개발 주기

### CI / CD

- Continuous Integration
  - Code -> Build -> Test
  - 테스트(개발과정, 개발 서버, 스테이지 서버, 프로덕션 서버)
- Continuous Delivery
  - Deploy + Management
  - CI -> Provision -> Deploy -> Monitor
- Provision
- 징에기 났을 때 자동으로 Rollback 하는 것도 중요하다.
- 빌드해서 테스트하는 서버 따로있고, 배포하는 서버 따로있다. (github action 처럼?)
- 요즘에는 인프라 관리를 쿠버네티스로 한다.

### AWS 운영 관리 툴

- Light Sail
  - heroku와 같이 사용이 쉽다.
- Elastic Beanstalk
  - 코드만으로 인프라를 관리해준다.
  - 스타트업에서 보통 사용한다.
- OpsWorks
  - EC2를 제어해주는 운영 툴
- CloudFormation
  - NASA가 사용하는 툴
  - 무료 어렵다.
  - JSON으로 인프라를 구성

#### 참고 링크

- https://lucas.codesquad.kr/main/course/masters-backend-java/DevOps/Intro-to-DevOps

