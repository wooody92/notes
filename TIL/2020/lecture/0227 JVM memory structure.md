### 오늘의 강의

1. 자바의 객체는 포인터(읽기전용)다.
2. 함수 하나 생성될 때마다 stack frame이 생성되고, 메인 함수 가장 아래 스택에 args가 쌓인다.
3. 자바에서는 참조변수 자체의 값(매개변수의 포인터 값)을 바꿀 수 없다 -> 리턴 값으로 받아 씀

#### JVM 메모리구조

```
https://lucas.codesquad.kr/course/masters-backend-java/강의자료-모음/JVM과-메모리
```

1. 클래스로더가 클래스파일을 메모리에 올린다.
2. 익스큐션 엔진이 실행한다.
   1. PC regiister : JVM에 프로그램 실행을 위해 필요한 자료구조 데이터들이 저장되어있음
   2. Stack Area : class new 하면 생성
   3. Heap Area : 
   4. Method Area : 상수 등
3. 톰캣 쓰레드는 멀티 쓰레드로 돌아가서, 스프링에서  한 객체에 여러 쓰레드가 접근가능
   1. Question question 충돌 가능성
4. 쓰레드별로 스택을 나눠서 쓴다.
