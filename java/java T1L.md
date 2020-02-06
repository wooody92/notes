### Java Today 1 Line (하루 한 줄 배움, Java에 대해 새로 알게된 사실 기록)

- Main 메서드에는 로직을 넣지 않는다. Main 메서드는 각 class들의 관계를 엮어주는 역할만 한다.

- Immutable과 mutable의 차이
```java
String str = "o"
for(int i=0; i<10000; i++){
  str += "o"
}

- String은 immutable하기 때문에, str이 반복문을 돌며 10000개의 객체가 생성된다. 즉, 10000개의 메모리를 잡아먹는다는 의미이다. 프로그램이 동작하고 garbage collector에 의해 정리되지만, g.c가 사용되는 순간 프로그램의 성능이 저하된다.
  
- 어떻게 개선할까?
  stringBuilder 혹은 stringBuffer은 mutable하기에 이를 사용하면 객체가 하나만 생성되기에 메모리를 절약할 수 있다.
```

