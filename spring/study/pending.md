## Exception 처리방식

1. ResponseEntity 공부하기

@ResponseBody나 ResponseEntity를 return 하는거나 결과적으로는 같은 기능이지만..그 구현 방법이 틀리죠..예를 들어 header 값을 변경시켜야 할 경우엔 @ResponseBody의 경우 파라미터로 Response 객체를 받아서 이 객체에서  header를 변경시켜야 하고..ResponseEntity에서는 이 클래스 객체를 생성한뒤 객체에서 header 값을 변경시키면 되죠.

https://github.com/kyungrae/java-qna/issues/3

https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc

-----

### JWT (Json Web Token)

https://velopert.com/2350

JWT 토큰 생성 및 검증 사이트

http://calebb.net/

예시

https://galid1.tistory.com/588

https://alwayspr.tistory.com/8

-----

