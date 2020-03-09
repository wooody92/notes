## JVM과 메모리 구조

- OS는 메인 메모리(RAM)을 관리한다.
- JVM이 실행되면 OS가 JVM에게 필요한 메모리를 할당해준다.
- JVM은 Runtime Data Area(OS로부터 할당받은 메모리) 크게 아래처럼 나누어 관리한다. (PC register, Native method stack 생략)

### Stack

- Heap 영역에 생성된 Object 타입의 데이터의 주소를 가리키는 참조값이(주소, 포인터 변수) 할당된다.
- 원시타입의 데이터가 값과 함께 할당된다. (메서드, 메서드 매개변수, 로컬변수, 원시타입(primitive type) 변수 ..)
- 각 Thread 는 자신만의 stack 을 가진다.
- 메서드가 실행될 때 스택에 쌓이고(push) 종료될 때 해제(pop)된다.

### Heap

- 모든 Object 타입(Integer, String, ArrayList, ...), 객체는 heap 영역에 생성된다.
- 힙 영역에 저장된 데이터는 메소드 호출이 끝나도 유지되며, 스택에서 가리키는 포인터값이 없으면 GC에 의해 메모리 해제된다.
- 몇개의 스레드가 존재하든 상관없이 단 하나의 heap 영역만 존재한다.
- Heap 영역에 있는 오브젝트들을 가리키는 레퍼런스 변수가 stack 에 올라가게 된다.
- 상속을 받으면 두 객체 모두 메모리에 올라간다. (A extend B에서 A 객체 생성하면 B도 함께 올라온다. )

### Method (Class, Static, Data) 

- 클래스 파일의 바이트 코드가 로드되는 곳이다.
- 프로그램을 실행 할 때 사용되는 클래스 파일들을 메모리에 올려놓는다.
- 어떤 메서드가 호출되면, 스태틱 영역에 로드된 클래스에서 해당 메서드 찾아 호출한다.
- 메인 메서드에서 사용하는 전역변수, 스태틱 등이 이 영역에 올라온다.

------

자바에서 Wrapper class 에 해당하는 Integer, Character, Byte, Boolean, Long, Double, Float, Short 클래스는 모두 Immutable 이다. 그래서 heap 에 있는 같은 오브젝트를 레퍼런스 하고 있는 경우라도, 새로운 연산이 적용되는 순간 새로운 오브젝트가 heap 에 새롭게 할당된다.

참고 블로그

```
https://yaboong.github.io/java/2018/05/26/java-memory-management/

https://wanzargen.tistory.com/16?category=700063

https://lucas.codesquad.kr/course/masters-backend-java/강의자료-모음/JVM과-메모리
```

