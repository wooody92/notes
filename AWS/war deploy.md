## 외부 톰캣 설치 및 war 배포

### Java war 설정

- 의존성 추가

  ```java
  plugins {
  	id 'org.springframework.boot' version '2.2.6.RELEASE'
  	id 'io.spring.dependency-management' version '1.0.9.RELEASE'
  	id 'java'
  	id 'war' // 추가
  }
  
  ...
  
  bootWar {
  	archiveFileName = "ROOT.war" // 빌드 시 해당 이름으로 war 파일이 생성된다.
  }
  
  ...
    
  dependencies {
  	implementation 'org.springframework.boot:spring-boot-starter-data-jdbc'
  	implementation 'org.springframework.boot:spring-boot-starter-web'
  	compileOnly 'org.projectlombok:lombok'
  	runtimeOnly 'com.h2database:h2'
  	runtimeOnly 'mysql:mysql-connector-java'
  	annotationProcessor 'org.projectlombok:lombok'
  	testImplementation('org.springframework.boot:spring-boot-starter-test') {
  		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
  	}
  	compile group: 'io.jsonwebtoken', name: 'jjwt', version: '0.9.1'
  	providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat' // 추가
  }
  ```

- 톰캣 초기화 설정

  ```java
  @SpringBootApplication
  public class Sidedish11Application extends SpringBootServletInitializer {
  
  	public static void main(String[] args) {
  		SpringApplication.run(Sidedish11Application.class, args);
  	}
  	
    // extends 만 해줘도 무방
  	@Override
  	protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
  		return builder.sources(Sidedish11Application.class);
  	}
  }
  ```

  

-----

### Tomcat 설치

- Apt 설치하면 파일이 자동 분산되어 관리하기가 힘들다. 그러므로 wget link 설치한다.

  현재 경로로 해당 파일 설치된다.

  ```
  wget http://apache.tt.co.kr/tomcat/tomcat-9/v9.0.34/bin/apache-tomcat-9.0.34.tar.gz
  ```

- 압축 풀기

  ```
  tar xvf apache-tomcat-9.0.34.tar.gz
  ```

- 성공적으로 실행되면 아래 디렉토리로 이동 할 수 있다.

  ```
  cd apache-tomcat-9.0.34/bin
  ```

- apache-tomcat-9.0.34/bin 경로에서 톰캣 실행 & 종료

  ```
  ./startup.sh
  ./shutdown.sh
  ```

- 톰캣 정상 실행 중인지 확인 한다.

  ```
  ps -ef | grep tomcat
  ```

-----

### war 배포

- git clone GitHub-url 에서 받은 디렉토리에서 빌드한다.

  ```
  ./gradlew bootWar -x test
  ```

- 정상 빌드 되면 /build/libs 경로에 jar가 아닌 war 파일이 생성된다.

  ```
  ROOT.war
  ```

- war 파일 톰캣 디렉토리로 이동

  특정한 디렉토리 (myDirectory)에 설치했다면 아래처럼 복사 가능하다.

  ```
  cp ROOT.war /apache-tomcat-9.0.34/webapps
  
  cp ROOT.war ~/myDirectory/apache-tomcat-9.0.34/webapps
  ```

- apache-tomcat-9.0.34/webapps 경로 확인하면 war 파일 생성되어 있다.

  ```
  drwxr-x---  7 ubuntu ubuntu     4096 Apr 28 12:31 .
  drwxrwxr-x  9 ubuntu ubuntu     4096 Apr 28 12:10 ..
  drwxr-x---  5 ubuntu ubuntu     4096 Apr 28 12:31 ROOT
  -rw-rw-r--  1 ubuntu ubuntu 24932609 Apr 28 12:31 ROOT.war
  drwxr-x--- 16 ubuntu ubuntu     4096 Apr 28 12:10 docs
  drwxr-x---  6 ubuntu ubuntu     4096 Apr 28 12:10 examples
  drwxr-x---  5 ubuntu ubuntu     4096 Apr 28 12:10 host-manager
  drwxr-x---  5 ubuntu ubuntu     4096 Apr 28 12:10 manager
  ```

- 톰캣은 demon으로 돌아가기 때문에 백그라운드 설정없이 AWS ssh 연결이 종료되어도 정상 동작한다. 



#### 참고링크

- [Lucas](https://lucas.codesquad.kr/course/마스터즈-프로젝트/학습자료-BE/spring-boot-war-deploy)
- [Sunny gist](https://github.com/codesquad-member-2020/sidedish-06/wiki/외부-tomcat-배포하기(war))
- https://www.youtube.com/watch?v=_GkOmt_3hjM&t=1014s
