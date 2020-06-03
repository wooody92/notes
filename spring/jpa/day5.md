# JPA 학습

## API 개발 기본

### 회원 등록 API

- `Template Engine`과 `API`는 공통 에러처리나 응답하는 양식이(`HTML`, `JSON`) 다르기 때문에 다른 `package`로 나누어서 처리하는 것이 좋다.
- `@RestController` = `@Controller` + `ResponseBody`(데이터를 바로 `JSON`이나 `XML`로 보낼 때 사용)
- `@Valid`를 사용하면 `@NotNull`과 같이 `Validation`관련 어노테이션을 전부 점검한다.

#### Version 1

- 엔티티를 웹 계층에 노출시키지 않고 DTO를 활용한다.
- 요청 파라미터를 Entity 타입 자체로 받는 것은(`@RequestBody Member member`) 엔티티 변경 시 API 스펙 자체가 바뀔 수 있고 장애 발생 위험이 크므로 사용하지 않도록 한다. 
- `@Valid`를 사용하여 `Validation package`  어노테이션들을 관리 할 수 있다. 

#### Version 2

- 요청 매개변수를 DTO를 이용하여 받는다.
- 엔티티는 외부에 노출하지 않는다.
- API 스펙이 변경 될 위험이 없다.

### 회언 수정 API

- P.K 기준으로 하나 조회하는 메서드의 경우 성능에 큰 영향을 끼치지 않기 때문에 유지보수 측면에서 커맨드와 쿼리를 분리해서 사용한다.

  ```java
  // 분리 전
  Member member = memberService.update(id, request.getName());
  
  // 분리 후
  memberService.update(id, request.getName());
  Member findMember = memberService.findOne(id);
  ```

### 회원 조회 API

- 절대 엔티티를 `presentation` 계층에 노출하지 않는다. 중간에 API에 맞는 DTO를 만들어서 사용하도록 한다.

