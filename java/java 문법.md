### 자주 까먹는 문법

- 특정문자 제거 혹은 대체

  ```
  str = str.replaceAll("remove part", "new" )
  ```

- 문자열 split 후 문자열 배열로 입력

  ```
  String[] arr = str.split("x")
  ```

  배열 출력

  https://seongsillvanas.tistory.com/9

- 10진수 -> 2진수 변환

  ```
  Integer.toBinaryString(10진수)
  ```

- Static 으로 선언 되있는 변수 혹은 메소드는 선언 된 큰 틀안에서만 사용 가능하다고 생각 (외부 참조불가)

- Scanner 보다 빠르다.

  ```
  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  int+Enter: Integer.parseInt(br.readLine());
  int: br.read();
  String: br.readLine();
  ```

- == : Call by reference / .equals() : Call by value

  https://kmj1107.tistory.com/entry/JAVA-문자열string-비교-equals와-의-차이점-equals의-반대
