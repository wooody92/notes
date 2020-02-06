#### Unit test (단위 테스트)

- 메서드 (기본 실행단위)

- 프로덕션 코드 (사용자가 이용하는 코드) / 테스트 코드

- 클래스는 덩어리가 작을 수록 좋고, 두괄식으로 작성

- 각각의 테스트는 독립적으로 돌아가야함, 모든 단위 테스트간 의존성이 생기면 안됨

- 단위 테스트를 반복적으로 실행해도 같은 결과가 나와야 함 (보통 DB 테스트시..)

- Junit4 예제

  ```java
  public class CalculatorTest { 
      private static Calculator c;
      @Before
      public void setup() {
          c = new Calculator(); // 매 테스트마다 객체를 새로 생성하여 의존성 줄임
          System.out.println("set up");
      }
      
      @Test
      public void add() {
          assertEqals(0, c.add(0,0));
      }
      
      @After
  }
  ```

- 테스트 코드를 위해 프로덕션 코드를 변경할 수 있음

  - random, bufferedReader 경우 메서드 안에있으면 테스트 불가하여 밖으로 새로 빼줘야하는 경우가 있음

- 랜덤함수를 가진 프로덕션 코드는 어떻게 단위 테스트 할까?

  1. Override 이용: nextInt()를 재 정의 (랜덤이 아닌 특정 정수만 리턴하도록 변경), 참 거짓 테스트

  2. Mockito 이용: 1번과 로직은 동일하지만, 정의되어진 mockito 사용
