### 오늘의 강의

1. 기능구현은 단순하게 그 기능만 수행하도록 먼저 구현 하기(미래에 생길 에러에 대해서는 나중에 추가)
2. 자바에는 call by reference(참조 변수)가 내부적으로는 없지만, 외부적으로는 있는 것 처럼 보이게 동작한다.
3. 자바에서 오브젝트를 call by reference로 하는 이유? -> 스택에 호출한 영역(메서드?) 복사해서 매개변수 값을 복사해서 불러오게 되는데, call by value로 하면 메모리 감당이 안되서 overhead 발생. 그래서 주소값만 참조해옴
4. primitive는 call by value로 고정, 나머지는 call by reference
5. 객체는 힙에 생성된다.

```
# C언어 기본구조
1. 지역변수(int a) 스택에 저장된다.
2. 함수를 생성하면, 스택에 새 영역이 생성된다.
3. 생성된 영역에 매개변수를 불러올 때 매개변수 값을 그대로 복사한다. 주소값 참조를 해서 메모리를 아낀다.
4. 모든 것은 call by value이고, 포인터를 이용해 call by reference 구현
5. Syntax sugar: 문법을 더 보기 쉽게 표현하는 것
	- 배열과 포인터는 동일한 것이다.
```

1. 스프링 MVC는 웹 프레임워크다.
2. 스프링이 갖고 있는 설계철학, OOP 등이 Java 언어를 좋은 방향으로 더 활용 할 수 있게 된다.
3. java bean: 재사용 가능한 자바 컴포넌트 -> 스프링 컨테이너 안에 들어감
4. 빈즈.. 싱글톤.. 
5. 쓰레드는 가벼운 프로세스.. 흐름의 단위..
6. 쓰레드는 쓰레드마다 PC, 스택이 필요하다.. 지역변수는 쓰레드를 공유 안한다.. 즉 지역변수는 외부 접근이 안되어서 안전하다..
7. 스프링 -> DI -> 빈즈 -> 싱글톤 -> 동기화에 유의하자
