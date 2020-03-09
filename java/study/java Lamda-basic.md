## 람다(lambda)

람다는 익명 함수의 다른 표현이다. 즉, 함수는 함수인데 이름이 없는 경우를 의미한다.

------

## Collection의 모든 값을 출력

```java
// next.fp.Lambda의 printAllOld method
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

for (int number : numbers) {
    System.out.println(number);
}
코드복사
```

------

## 람다가 없던 시절

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

numbers.forEach(new Consumer<Integer>() {
    public void accept(Integer value) {
        System.out.println(value);
    }
});
코드복사
```

------

## 람다를 활용하면…

```java
// next.fp.Lambda의 printAllLambda method
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

numbers.forEach((Integer value) -> System.out.println(value));
numbers.forEach(value -> System.out.println(value)); // Type 추론이 가능해 Type 생략 가능
numbers.forEach(System.out::println); // :: 연산자 활용 가능
= numbers.forEach(x -> System.out.println(x));
코드복사
```

------

## 람다 문법

input arguments -> body

------

## 람다 실습

- 다음 테스트 코드에서 MoveStrategy에 대한 익명 클래스로 구현하고 있는데 람다를 적용해 구현한다.

```java
// next.fp.CarTest의 이동, 정지 method
public class CarTest {
    @Test
    public void 이동() {
        Car car = new Car("pobi", 0);
        Car actual = car.move(new MoveStrategy() {
            @Override
            public boolean isMovable() {
                return true;
            }
        });
        assertEquals(new Car("pobi", 1), actual);
    }
코드복사
```

------

```java
    @Test
    public void 정지() {
        Car car = new Car("pobi", 0);
        Car actual = car.move(new MoveStrategy() {
            @Override
            public boolean isMovable() {
                return false;
            }
        });
        assertEquals(new Car("pobi", 0), actual);
    }
}
코드복사
```

-----

## 람다를 통한 중복 제거
### 예제 실습

```java
        public static int sumAll(List<Integer> numbers) {
//     CASE 1
//         int total = 0;
//         for (int number : numbers) {
//             total += number;
//         }
//     CASE 2
//         numbers.stream().reduce(Integer::sum).get();

           return sum(numbers, number -> true);
       }

       public static int sumAllEven(List<Integer> numbers) {
//     CASE 1
//         int total = 0;
//         for (int number : numbers) {
//             if (number % 2 == 0) {
//                 total += number;
//             }
//         }

//     CASE 2
//         numbers.stream().reduce(0, (a, b)-> (b%2==0) ? a+b : a);

              return sum(numbers, number -> (number%2==0) ? true : false);

       }

       public static int sumAllOverThree(List<Integer> numbers) {
//     CASE 1
//         int total = 0;
//         for (int number : numbers) {
//            if (number > 3) {
//                   total += number;
//            }
//         }
//     CASE 2
//         numbers.stream().reduce(0, (a, b)-> (b>3) ? a+b : a);

           return sum(numbers,number -> (number>3) ? true : false);
       }
       
       // Java에 아래와 같은 기본 인터페이스는 내장되어있음
       public interface Conditional {
              boolean test(Integer number);
       }

       public static int sum(List<Integer> numbers, Conditional c) {
              int total = 0;
              for (int number : numbers) {
                     if (c.test(number)) {
                            total += number;
                     }
              }
              return total;
       }
```

-----

