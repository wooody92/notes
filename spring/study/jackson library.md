## Jackson

### Jackson 라이브러리?

- `Jackson`은 `JSON` 데이터 구조를 처리해주는 라이브러리다.
- `Spring` 개발을 하다 보면, 컨트롤러 ***text/html\*** 형식이 아닌 데이터 전달 목적으로 사용하고 싶을 때가 있다. 물론, 쌩 문자열인 ***plain/text\*** 형식으로 보내도 상관은 없다만, 보통은 데이터 구조를 표현하는 방식인 `XML` 또는 `JSON` 형태로 많이 보낸다.

### Jackson의 데이터 매핑

- getter : Jackson 라이브러리가 default로 getter 메서드가 있는 entity만 Json 변환한다.
- @JsonProperty : getter가 없어도 해당 entity Json 변환한다.
- @JsonIgnore : getter 메서드에 있어도, @JsonIgnore 추가하면 변환하지 않는다.
- @RestController
  - 반환된 객체를 JSON 타입으로 변환을 하기 위해 사용한다.

#### 참고 블로그

https://mommoo.tistory.com/83
