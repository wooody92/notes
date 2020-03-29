## Spring 인프런 (백기선)

> 강의 링크
> https://www.inflearn.com/course/spring_revised_edition#

### Pet Clinic

- Dispatcher sevlet 역할이란?

- Bean : 스프링이 관리하는 객체

- %:firstName% 중간글자 검색

- ```java
  @Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.firstName LIKE %:firstName%")
  @Transactional(readOnly = true)
  Collection<Owner> findByFirstName(@Param("firstName") String firstName);
  ```
-----
## * Spring Triangle

## 1.스프링 IoC

### IoC (Inversion of Controll)

- 제어권의 역전
- 내가 사용할 의존성을 다른 곳에 위임하는 것
- 스프링의 IoC 컨테이너가 빈들의 의존성을 관리해준다. 즉, 객체를 만들어 빈으로 만들고 그 빈들의 필요한 의존성을 어노테이션, 생성자 등을 통해 주입해준다.

### IoC Container

- BeanFactory, ApplicationContext
- 역할 : 빈을 만들고 의존성을 엮어주며 제공해준다.
- 의존성 주입은 컨테이너 안에 있는 빈 끼리만 가능하다.
- 싱글톤으로 쉽게 만들어준다.

### Bean

- IoC가 관리하는 객체

- applicationContext가 갖고있는 객체만 빈이다.

- 어떻게 빈으로 등록할까?

  - @SpringBootApplication - @ComponentScan에서 선언 된 곳의 하위 패키지 클래스의 Component를 Scan 한다.

  - Component Scanning

    ```java
    @Component
    @Repository
    @Service
    @Controller
    @Configuration
    ```

  - XML, 자바 설정 파일에 등록

    아래는 SampleController 클래스를 설정파일을 통해 빈으로 등록하는 예시이다.

    ```java
    @Configuration
    public class SampleConfig() {
      @Bean
      public SampleController sampleController() {
        return new SampleController();
      }
    }
    ```

### D.I. (의존성 주입)

- 빈이 아닌 객체에 의존성을 주입하려하면, No qualifying bean of type 에러 발생
- 생성자 : 가장 권장되는 수단이다. 그러나 순환참조 문제 발생하면 필드 인젝션으로 처리 가능하다.
- Setter (with @Autowired)
- 필드에서 주입 : @Autowired

-----

## 2.스프링 AOP

### AOP (Aspect Oriented Programming)

- 객체지향적 프로그래밍
- 다양한 AOP 구현방법
  - 컴파일 : A.java --(AOP)--> A.class (AspectJ 참고)
  - 바이트코드 조작 : A.java --> A.class --(AOP)--> 메모리 (AspectJ 참고)
  - 프록시 패턴 (스프링 AOP)

### 프록시 패턴

- 기존 코드는 건들이지 않고 새 기능 추가하 기
- @Transactional
- 클래스를 생성하여 기존 타겟 클래스가 사용하는 인터페이스를 상속받아 새로 정의 후 사용

-----

## 3.스프링 PSA

### PSA (Portable Service Apstraction)

- 편리한 인터페이스, 편의성을 제공
- 스프링 부트에서 코드를 작성할 때 따로 서블릿 동작 코드를 작성하지 않고 사용해도 잘 작동한다.
- 그 이유는 인터페이스 추상화로 잘 구현이 되어있고, 서블릿은 그 기반에서 작성되어 구동되기 때문이다.
- 서블릿 / 리액티브, 톰캣 / 네티
- 스프링 웹 MVC, 스프링 트랜잭션, 스프링 캐시
- Transaction : All or nothing (A, B, C 전부 진행되야 동작, 하나라도 안되면 동작하지 않음)
