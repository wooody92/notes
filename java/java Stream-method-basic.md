## 스트림 메서드

## map, filter, reduce

------

- Collection에 담긴 데이터를 처리하려면 Collection을 순회하면서 각 Element를 처리하는 것이 일반적이다.
- 앞으로는 순회하는 것을 잊고, Element 처리에만 집중하자.

------

## filter

요구사항은 파일 문자 중 길이가 12보다 큰 문자의 수를 구한다.

```java
// next.fp.StreamStudy countWords method

String contents = new String(Files.readAllBytes(
  Paths.get("../ war-and-peace.txt")), StandardCharsets.UTF_8);
List<String> words = Arrays.asList(contents.split("[\\P{L}]+"));

long count = 0;
for (String w : words) {
  if (w.length() > 12) count++;  
}
코드복사
```

------

## filter 활용해 구현

```
String contents = new String(Files.readAllBytes(
  Paths.get("../alice.txt")), StandardCharsets.UTF_8);
List<String> words = Arrays.asList(contents.split("[\\P{L}]+"));

long count = 
  words.stream().filter(w -> w.length() > 12).count();
코드복사
```

------

## map

List에 담긴 모든 숫자 값을 2배한 결과 List를 생성한다.

```
// next.fp.StreamStudy 클래스의 doubleNumbers method 참고
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
List<Integer> dobuleNumbers =
  numbers.stream().map(x -> 2 * x).collect(Collectors.toList());
코드복사
```

------

## reduce

List에 담긴 모든 숫자의 합을 구한다.

```
// next.fp.StreamStudy 클래스의 sumAll method 참고

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

public int sumAll(List<Integer> numbers) {
    return numbers.stream().reduce(0, (x, y) -> x + y);
}
```
